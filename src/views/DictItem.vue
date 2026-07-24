<template>
    <section class="dict-item" :class="{ open: isOpen, expand: isExpand, loading: isLoading }">
        <header class="dict-item-header" @click="onOpen">
            <div :class="['dict-icon', props.id]"></div>
            <span class="dict-name">{{ props.name }}</span>
            <div class="dict-loading">
                searching...
            </div>
            <div class="empty-area"></div>
            <button class="fold-arrow-btn" aria-label="Toggle dictionary">
                <svg class="fold-arrow" width="12" height="12" viewBox="0 0 59.414 59.414"
                    xmlns="http://www.w3.org/2000/svg">
                    <path class="dictItemHead-FoldArrowPath"
                        d="M43.854 59.414L14.146 29.707 43.854 0l1.414 1.414-28.293 28.293L45.268 58"></path>
                </svg>
            </button>
        </header>
        <div class="dict-item-body">
            <article>
                <slot></slot>
            </article>
            <button class="fold-mask" @click="onExpand">
                <svg class="fold-mask-arrow" width="14" height="14" viewBox="0 0 59.414 59.414"
                    xmlns="http://www.w3.org/2000/svg">
                    <path d="M58 14.146L29.707 42.44 1.414 14.145 0 15.56 29.707 45.27 59.414 15.56"></path>
                </svg>
            </button>
        </div>
    </section>
</template>

<script setup lang="ts">
import { ref, watch, getCurrentInstance, toRef } from "vue";
import PluginType from "@/plugin";

const plugin = getCurrentInstance().appContext.config.globalProperties
    .plugin as PluginType;
let defaultHeight = toRef(plugin.store, "dictHeight");

let isOpen = ref(false);
let isExpand = ref(false);
let isLoading = ref(false);

const props = defineProps<{
    loading: boolean;
    name: string;
    id: string;
}>();

watch(
    () => props.loading,
    (loading) => {
        isLoading.value = loading;
        if (loading) {
            isOpen.value = false;
            isExpand.value = false;
        } else {
            isOpen.value = true;
        }
    }
);

function onOpen() {
    if (isOpen.value) {
        isOpen.value = false;
        isExpand.value = false;
    } else {
        isOpen.value = true;
    }
}

function onExpand() {
    isExpand.value = true;
}
</script>

<style lang="scss">
.dict-item {
    margin-bottom: 2px;
    interpolate-size: allow-keywords;

    header.dict-item-header {
        display: flex;
        align-items: center;
        position: relative;
        position: sticky;
        top: 0;
        z-index: 100;
        border-top: 1px solid var(--background-modifier-border, var(--divider-color, rgba(128, 128, 128, 0.25)));
        background-color: var(--background-secondary);
        height: 24px;
        padding: 0 4px;
        cursor: pointer;
        user-select: none;

        &::before {
            content: "";
            position: absolute;
            inset: 0;
            background-color: var(--background-modifier-hover);
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.15s ease;
            z-index: 0;
        }

        &:hover::before {
            opacity: 1;
        }

        .dict-icon,
        .dict-name,
        .dict-loading,
        .empty-area,
        .fold-arrow-btn {
            position: relative;
            z-index: 1;
        }

        .dict-icon {
            height: 16px;
            width: 16px;
            background-size: cover;
            flex-shrink: 0;
        }

        .dict-name {
            padding-left: 6px;
            font-size: 0.92em;
            font-weight: 500;
            color: var(--text-normal);
            line-height: 24px;
        }

        .dict-loading {
            font-size: 0.85em;
            color: var(--text-muted);
            padding-left: 12px;
            font-style: italic;
        }

        .empty-area {
            flex: 1;
        }

        .fold-arrow-btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            color: var(--text-muted);
            width: 18px;
            height: 18px;
            background: transparent;
            border: none;
            padding: 0;
            cursor: pointer;
            box-shadow: none;
            border-radius: 3px;

            &:hover {
                box-shadow: none;
                background-color: var(--background-modifier-hover);
            }

            .fold-arrow {
                transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1);
                fill: var(--text-muted);
            }
        }
    }

    .dict-item-body {
        position: relative;
        overflow: hidden;
        padding: 0;
        background-color: var(--background-secondary);
        transition: height 0.35s cubic-bezier(0.4, 0, 0.2, 1);
        height: 0;

        article {
            padding: 6px 4px 4px 4px;
            background-color: var(--background-secondary);
        }

        .fold-mask {
            position: absolute;
            left: 0;
            bottom: 0;
            width: 100%;
            height: 32px;
            z-index: 10;
            padding: 0;
            border: none;
            box-shadow: none;
            background: linear-gradient(
                to bottom,
                transparent 0%,
                var(--background-secondary) 85%
            );
            cursor: pointer;
            display: flex;
            align-items: flex-end;
            justify-content: center;
            padding-bottom: 2px;

            .fold-mask-arrow {
                fill: var(--text-muted);
                transition: fill 0.15s ease, transform 0.15s ease;
            }

            &:hover .fold-mask-arrow {
                fill: var(--text-normal);
                transform: translateY(1px);
            }
        }
    }

    &:not(.open) {
        .fold-mask {
            display: none;
        }

        .dict-item-body {
            height: calc-size(0px, size);
        }
    }

    &.open {
        .fold-arrow {
            transform: rotate(-90deg);
        }
    }

    &.open:not(.expand) {
        .dict-item-body {
            height: calc-size(auto, min(size, v-bind(defaultHeight)));
        }
    }

    &.expand {
        .fold-mask {
            display: none;
        }

        .dict-item-body {
            height: calc-size(auto, size);
            transition: height 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }
    }

    &:not(.loading) {
        .dict-loading {
            display: none;
        }
    }
}
</style>
