<template>
    <transition name="fade">
        <div
            v-if="visible"
            class="fixed top-5 right-5 z-50 flex items-center w-full max-w-xs p-4 mb-4 text-gray-500 bg-white rounded-lg shadow"
            role="alert"
        >
            <div
                class="inline-flex items-center justify-center flex-shrink-0 w-8 h-8 rounded-lg"
                :class="iconBackground"
            >
                <component :is="icon" class="w-5 h-5" :class="iconColor" />
            </div>
            <div class="ml-3 text-sm font-medium">{{ message }}</div>
            <button
                type="button"
                class="ml-auto -mx-1.5 -my-1.5 bg-white text-gray-400 hover:text-gray-900 rounded-lg p-1.5"
                @click="close"
            >
                <span class="sr-only">Close</span>
                ✕
            </button>
        </div>
    </transition>
</template>

<script setup>
import {ref, onMounted, h} from 'vue'

// Props
const props = defineProps({
    type: {
        type: String,
        default: 'success', // success, error, warning, info
    },
    message: {
        type: String,
        required: true,
    },
    duration: {
        type: Number,
        default: 3000,
    },
})

// Icon logic
const icons = {
    success: {
        icon: {
            render() {
                return h('svg', {
                    class: 'w-5 h-5',
                    fill: 'none',
                    stroke: 'currentColor',
                    strokeWidth: 2,
                    viewBox: '0 0 24 24',
                    innerHTML: '<path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />',
                })
            },
        },
        bg: 'bg-green-100',
        color: 'text-green-500',
    },
    error: {
        icon: {
            render() {
                return h('svg', {
                    class: 'w-5 h-5',
                    fill: 'none',
                    stroke: 'currentColor',
                    strokeWidth: 2,
                    viewBox: '0 0 24 24',
                    innerHTML: '<path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />',
                })
            },
        },
        bg: 'bg-red-100',
        color: 'text-red-500',
    },
    warning: {
        icon: {
            render() {
                return h('svg', {
                    class: 'w-5 h-5',
                    fill: 'none',
                    stroke: 'currentColor',
                    strokeWidth: 2,
                    viewBox: '0 0 24 24',
                    innerHTML: '<path stroke-linecap="round" stroke-linejoin="round" d="M12 9v2m0 4h.01M4.93 4.93l14.14 14.14" />',
                })
            },
        },
        bg: 'bg-yellow-100',
        color: 'text-yellow-500',
    },
    info: {
        icon: {
            render() {
                return h('svg', {
                    class: 'w-5 h-5',
                    fill: 'none',
                    stroke: 'currentColor',
                    strokeWidth: 2,
                    viewBox: '0 0 24 24',
                    innerHTML: '<path stroke-linecap="round" stroke-linejoin="round" d="M13 16h-1v-4h-1m1-4h.01" />',
                })
            },
        },
        bg: 'bg-blue-100',
        color: 'text-blue-500',
    },
}

const {icon, bg: iconBackground, color: iconColor} = icons[props.type] || icons.success

// State
const visible = ref(true)
const emit = defineEmits(['closed'])

function close() {
    visible.value = false
    emit('closed')
}

onMounted(() => {
    setTimeout(close, props.duration)
})
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>
