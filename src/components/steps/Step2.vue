<!-- Step2.vue -->
<template>
    <div>
        <div class="text-center mb-6">
            <h2 class="text-2xl font-bold text-gray-800">Describe Your Website</h2>
            <p class="text-gray-500 mt-2">Tell us the primary purpose of your website</p>
        </div>

        <form class="space-y-4">
            <div class="mb-2">
                <h3 class="text-lg font-semibold text-gray-800">Website Type</h3>
            </div>

            <div class="space-y-3">
                <div v-for="websiteType in websiteTypes" :key="websiteType" class="flex items-center">
                    <input
                        :id="`websiteType-${websiteType}`"
                        type="radio"
                        :value="websiteType"
                        v-model="modelValue.websiteType"
                        class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500"
                    />
                    <label :for="`websiteType-${websiteType}`" class="ml-2 text-sm text-gray-700">
                        {{ websiteType }}
                    </label>
                </div>
                <span class="text-red-800" v-if="errors.websiteType">{{ errors.websiteType }}</span>
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
    websiteTypes: Array,
})

defineEmits(['next', 'back'])

const schema = yup.object({
    websiteType: yup.string().required('Website type is required'),
})
</script>
