<!-- Step3.vue -->
<template>
    <div>
        <div class="text-center mb-6">
            <h2 class="text-2xl font-bold text-gray-800">Choose Your Platform</h2>
            <p class="text-gray-500 mt-2">Select the platform your website is built or planned on</p>
        </div>

        <form class="space-y-4">
            <div class="text-center mb-4">
                <h3 class="text-lg font-semibold text-gray-800">Select Platform</h3>
            </div>

            <div class="space-y-3">
                <div v-for="platform in platformTypes" :key="platform" class="flex items-center">
                    <input
                        :id="`platform-${platform}`"
                        type="radio"
                        :value="platform"
                        v-model="modelValue.platform"
                        class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500"
                    />
                    <label :for="`platform-${platform}`" class="ml-2 text-sm text-gray-700">
                        {{ platform }}
                    </label>
                </div>
                <span class="text-red-800" v-if="errors.platform">{{ errors.platform }}</span>
            </div>

            <div class="pt-6 flex justify-between">
                <button
                    type="button"
                    @click="$emit('back')"
                    class="bg-gray-300 text-gray-700 py-2 px-4 rounded-md hover:bg-gray-400 transition"
                >
                    Back
                </button>
                <button
                    type="button"
                    @click="$emit('next', schema)"
                    class="bg-blue-600 text-white py-2 px-6 rounded-md hover:bg-blue-700 transition"
                >
                    Next
                </button>
            </div>
        </form>
    </div>
</template>

<script setup>
import * as yup from 'yup'

defineProps({
    modelValue: Object,
    errors: Object,
    platformTypes: Array,
})

defineEmits(['next', 'back'])

const schema = yup.object({
    platform: yup.string().required('Platform is required'),
})
</script>
