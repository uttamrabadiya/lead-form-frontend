<!-- ReviewStep.vue -->
<template>
    <div>
        <div class="text-center mb-6">
            <h2 class="text-2xl font-bold text-gray-800">Review Your Details</h2>
            <p class="text-gray-500 mt-2">Make sure everything is correct before submitting</p>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div>
                <p class="text-sm text-gray-500">Name</p>
                <p class="font-medium text-gray-900">{{ form.name }}</p>
            </div>
            <div>
                <p class="text-sm text-gray-500">Email</p>
                <p class="font-medium text-gray-900">{{ form.email }}</p>
            </div>
            <div>
                <p class="text-sm text-gray-500">Company Name</p>
                <p class="font-medium text-gray-900">{{ form.companyName }}</p>
            </div>
            <div>
                <p class="text-sm text-gray-500">Website</p>
                <p class="font-medium text-gray-900">{{ form.website }}</p>
            </div>
            <div>
                <p class="text-sm text-gray-500">Platform</p>
                <p class="font-medium text-gray-900">{{ form.platform }}</p>
            </div>
            <div>
                <p class="text-sm text-gray-500">Website Type</p>
                <p class="font-medium text-gray-900">{{ form.websiteType }}</p>
            </div>
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
                @click="$emit('submit')"
                class="bg-blue-600 text-white py-2 px-6 rounded-md hover:bg-blue-700 transition"
            >
                Submit
            </button>
        </div>
    </div>
</template>

<script setup>
defineProps({
    form: Object
})

defineEmits(['submit', 'back'])
</script>
