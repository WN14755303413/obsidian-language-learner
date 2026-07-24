<template>
    <div id="langr-search" @click="handleClick">
        <NConfigProvider :theme="theme" :theme-overrides="themeConfig">
            <div class="search-bar">
                <NButtonGroup size="small">
                    <NButton tag="div" :disabled="historyIndex <= 0" @click="switchHistory('prev')">{{ `<` }} </NButton>
                    <NButton tag="div" :disabled="historyIndex >= lastHistory" @click="switchHistory('next')">{{ ">" }}
                    </NButton>
                </NButtonGroup>
                <NInput size="small" type="text" placeholder="输入单词" v-model:value="inputWord" style="flex:1;"
                    @keydown.enter="handleSearch" />
                <NButton tag="div" circle size="small" @click="handleSearch" aria-label="Search">
                    <template #icon>
                        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                            <circle cx="11" cy="11" r="8"></circle>
                            <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
                        </svg>
                    </template>
                </NButton>
            </div>
        </NConfigProvider>
        <div class="dict-area" style="overflow:auto;">
            <DictItem v-for="(cp, i) in components" :loading="loadings[i]" :name="cp.name" :key="cp.id" :id="cp.id">
                <KeepAlive>
                    <Component @loading="loading" :is="cp.type" :word="word" v-show="shows[i]"></Component>
                </KeepAlive>
            </DictItem>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, shallowRef, computed, watch, onMounted, onUnmounted, getCurrentInstance } from "vue";
import { NConfigProvider, NButton, NButtonGroup, NInput, darkTheme, GlobalThemeOverrides } from "naive-ui";

import DictItem from "./DictItem.vue";
import { t } from "@/lang/helper";
import PluginType from "@/plugin";
import { dicts } from "@dict/list";
import { playAudio } from "@/utils/helpers";

const plugin = getCurrentInstance().appContext.config.globalProperties.plugin as PluginType;

const themeConfig: GlobalThemeOverrides = {

};

let components = shallowRef([]);
let map: { [K in string]: number } = {};
let loadings = ref<boolean[]>([]);
let shows = ref<boolean[]>([]);
watch(() => plugin.store.dictsChange, () => {
    let collection = Object.keys(dicts)
        .map((dict: keyof typeof dicts) => {
            return {
                id: dict,
                priority: plugin.settings.dictionaries[dict].priority,
                name: dicts[dict].name,
            };
        })
        .filter((dict) => plugin.settings.dictionaries[dict.id].enable);
    collection.sort((a, b) => a.priority - b.priority);

    components.value = collection.map((dict) => {
        return {
            id: dict.id,
            name: dict.name,
            type: dicts[dict.id].Cp,
        };
    });
    collection.forEach((v, i) => {
        map[v.id] = i;
    });
    loadings.value = Array(collection.length).fill(false);
    shows.value = Array(collection.length).fill(false);

}, {
    immediate: true
});

function loading({ id, loading, result }: { id: string, loading: boolean, result: boolean; }) {
    loadings.value[map[id]] = loading;
    shows.value[map[id]] = result;
}

// 切换明亮/黑暗模式
const theme = computed(() => {
    return plugin.store.dark ? darkTheme : null;
});

// 提供一个前进后退查询记录的功能
let history: string[] = [];
let lastHistory = ref(history.length - 1);
let historyIndex = ref(-1);
function switchHistory(direction: "prev" | "next") {
    historyIndex.value = Math.max(
        0,
        Math.min(historyIndex.value + (direction === "prev" ? -1 : 1), history.length - 1)
    );
    word.value = history[historyIndex.value];
    inputWord.value = history[historyIndex.value];
}
function appendHistory() {
    if (historyIndex.value < history.length - 1) {
        history = history.slice(0, historyIndex.value + 1);
    }
    history.push(word.value);
    lastHistory.value = history.length - 1;
    historyIndex.value++;
}

let inputWord = ref("");
let word = ref("");
const onSearch = async (evt: CustomEvent) => {
    let text = evt.detail.selection;
    word.value = text;
    appendHistory();
};

function handleSearch() {
    word.value = inputWord.value;
    appendHistory();
}

function handleClick(evt: MouseEvent) {
    const target = evt.target as HTMLElement;
    if (target.hasClass("speaker")) {
        evt.preventDefault();
        evt.stopPropagation();
        let url = (target as HTMLAnchorElement).href;
        playAudio(url);

    }
    else if (target.tagName === "A") {
        evt.preventDefault();
        evt.stopPropagation();
        word.value = target.textContent;
        inputWord.value = target.textContent;
        appendHistory();
    }
}


onMounted(() => {
    addEventListener('obsidian-langr-search', onSearch);
});

onUnmounted(() => {
    removeEventListener('obsidian-langr-search', onSearch);
});
</script>

<style lang="scss">
#langr-search {
    height: 100%;
    width: 100%;
    overflow: hidden;
    font-size: 0.9em;
    user-select: text;
    display: flex;
    flex-direction: column;

    .search-bar {
        padding: 4px;
        display: flex;
        align-items: center;
        gap: 4px;
    }

    .dict-area {
        flex: 1;
        padding-left: 4px;
        overflow-y: auto;
        scrollbar-gutter: stable;
        scrollbar-width: thin;
        scrollbar-color: var(--scrollbar-thumb-bg, rgba(128, 128, 128, 0.25)) transparent;

        &::-webkit-scrollbar {
            width: 6px;
        }

        &::-webkit-scrollbar-thumb {
            background-color: var(--scrollbar-thumb-bg, rgba(128, 128, 128, 0.25));
            border-radius: 3px;

            &:hover {
                background-color: var(--scrollbar-active-thumb-bg, rgba(128, 128, 128, 0.45));
            }
        }

        &::-webkit-scrollbar-track {
            background: transparent;
        }
    }
}

.is-mobile #langr-search {
    button:not(.fold-mask) {
        width: auto;
    }

    input[type='text'] {
        padding: 0;
    }
}
</style>
