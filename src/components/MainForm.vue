<template>
    <div class="min-h-screen flex items-center justify-center bg-gray-100 px-4 py-8">
        <div class="bg-white rounded-lg shadow-lg w-full max-w-xl p-8 relative">

            <!-- Step Progress Indicator -->
            <StepIndicator :steps="steps" :current-step="step" />

            <!-- Step Components -->
            <Step1 v-if="step === 1" v-model="form" :errors="errors" @next="goToNextStep" />
            <Step2 v-if="step === 2" v-model="form" :errors="errors" :website-types="websiteTypes" @next="goToNextStep" @back="goBack" />
            <Step3 v-if="step === 3" v-model="form" :errors="errors" :platform-types="platformTypes" @next="goToNextStep" @back="goBack" />
            <ReviewStep v-if="step === 4" :form="form" @submit="submitForm" @back="goBack" />

            <Loader v-if="loading" />
            <Toast v-if="toastMessage" :type="toastType" :message="toastMessage" :duration="3000" @closed="toastMessage = ''" />

        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import apiClient from './../services/axios'
import Step1 from './steps/Step1.vue'
import Step2 from './steps/Step2.vue'
import Step3 from './steps/Step3.vue'
import ReviewStep from './steps/ReviewStep.vue'
import StepIndicator from './steps/StepIndicator.vue'
import Loader from './Loader.vue'
import Toast from './Toast.vue'

const step = ref(1)
const loading = ref(false)
const toastMessage = ref('')
const toastType = ref('success')
const steps = ['Basic Info', 'Website Details', 'Platform', 'Review & Submit']

const websiteTypes = ['E-commerce', 'Blog/Content Site', 'Corporate/Business Site', 'Portfolio', 'Other']
const platformTypes = ref([])

const form = ref({
    name: '',
    email: '',
    companyName: '',
    website: '',
    websiteType: null,
    platform: null
})

const errors = ref({})

function showToast(msg, type = 'success') {
    toastMessage.value = msg
    toastType.value = type
}

function goBack() {
    if (step.value > 1) step.value--
}

function goToNextStep(validationSchema) {
    validationSchema.validate(form.value, { abortEarly: false })
        .then(() => {
            if (step.value === 2) {
                loading.value = true
                apiClient.get('/api/platforms', { params: { websiteType: form.value.websiteType } })
                    .then(response => {
                        platformTypes.value = response.data.platforms || []
                        step.value++
                        loading.value = false
                    })
                    .catch(() => {
                        showToast('Failed to load platform types', 'error')
                        loading.value = false
                    })
            } else {
                step.value++
            }
            errors.value = {}
        })
        .catch(err => {
            const errorMap = {}
            err.inner.forEach(error => {
                if (error.path && !errorMap[error.path]) {
                    errorMap[error.path] = error.message
                }
            })
            errors.value = errorMap
        })
}

function resetForm() {
    form.value = {
        name: '',
        email: '',
        companyName: '',
        website: '',
        websiteType: null,
        platform: null
    }
    errors.value = {}
    step.value = 1
}

function submitForm() {
    loading.value = true
    apiClient.post('/api/lead', form.value)
        .then(() => {
            resetForm()
            showToast('We have received your data successfully!', 'success')
            loading.value = false
        })
        .catch(() => {
            showToast('Failed to submit form. Please try again later.', 'error')
            loading.value = false
        })
}
</script>
