<template>
    <div>
        <div class="text-center mb-6">
            <h2 class="text-2xl font-bold text-gray-800">Enter Your Details</h2>
            <p class="text-gray-500 mt-2">Basic details about you and your business</p>
        </div>
        <form class="space-y-4">
            <div class="flex flex-col gap-4">
                <div>
                    <label for="name" class="block mb-1 text-sm font-medium text-gray-700">Name</label>
                    <input type="text" id="name" v-model="modelValue.name"
                           class="form-input w-full border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" />
                    <span class="text-red-800" v-if="errors.name">{{ errors.name }}</span>
                </div>
                <div>
                    <label for="email" class="block mb-1 text-sm font-medium text-gray-700">Email</label>
                    <input type="email" id="email" v-model="modelValue.email"
                           class="form-input w-full border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" />
                    <span class="text-red-800" v-if="errors.email">{{ errors.email }}</span>
                </div>
                <div>
                    <label for="companyName" class="block mb-1 text-sm font-medium text-gray-700">Company Name</label>
                    <input type="text" id="companyName" v-model="modelValue.companyName"
                           class="form-input w-full border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" />
                    <span class="text-red-800" v-if="errors.companyName">{{ errors.companyName }}</span>
                </div>
                <div>
                    <label for="website" class="block mb-1 text-sm font-medium text-gray-700">Website</label>
                    <input type="url" id="website" v-model="modelValue.website"
                           class="form-input w-full border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500"
                           placeholder="https://example.com" />
                    <span class="text-red-800" v-if="errors.website">{{ errors.website }}</span>
                </div>
            </div>
            <div class="pt-4">
                <button type="button"
                        @click="$emit('next', schema)"
                        class="w-full bg-blue-600 text-white py-2 rounded-md hover:bg-blue-700 transition">Next</button>
            </div>
        </form>
    </div>
</template>

<script setup>
import * as yup from 'yup'
const props = defineProps({
    modelValue: Object,
    errors: Object
})
const emit = defineEmits(['next'])

const schema = yup.object({
    name: yup.string().required('Name is required'),
    email: yup.string().email('Invalid email').required('Email is required'),
    companyName: yup.string().required('Company Name is required'),
    website: yup.string().optional().url('Invalid Website URL'),
})
</script>
