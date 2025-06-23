<template>
    <div class="min-h-screen flex items-center justify-center bg-gray-100 px-4 py-8">
        <div class="bg-white rounded-lg shadow-lg w-full max-w-xl p-8 relative">
            <!-- Step Progress Indicator -->
            <div class="flex justify-between items-center mb-8">
                <div v-for="(label, index) in steps" :key="index" class="flex-1 flex items-center flex-col gap-2 text-center">
                    <!-- Circle -->
                    <div
                        class="flex items-center justify-center w-8 h-8 rounded-full text-white text-sm font-medium z-10"
                        :class="{
        'bg-blue-600': step > index,
        'bg-blue-500': step === index + 1,
        'bg-gray-300': step < index + 1
      }"
                    >
                        {{ index + 1 }}
                    </div>

                    <!-- Label -->
                    <div>
                        <p
                            class="text-sm font-medium"
                            :class="{
          'text-blue-600': step >= index + 1,
          'text-gray-400': step < index + 1
        }"
                        >
                            {{ label }}
                        </p>
                    </div>

                    <!-- Line -->
                    <div
                        v-if="index !== steps.length - 1"
                        class="flex-1 h-0.5 mx-4"
                        :class="{
        'bg-blue-600': step > index + 1,
        'bg-gray-300': step <= index + 1
      }"
                    ></div>
                </div>
            </div>


            <div v-if="step === 1" >
                <!-- Title and Description -->
                <div class="text-center mb-6">
                    <h2 class="text-2xl font-bold text-gray-800">Enter Your Details</h2>
                    <p class="text-gray-500 mt-2">Basic details about you and your business</p>
                </div>

                <!-- Step 1 -->
                <form class="space-y-4">
                    <div class="flex flex-col gap-4">
                        <div>
                            <label for="name" class="block mb-1 text-sm font-medium text-gray-700">Name</label>
                            <input type="text" id="name" v-model="form.name"
                                   class="form-input w-full border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" />
                            <span class="text-red-800" v-if="errors.name">{{errors.name}}</span>
                        </div>
                        <div>
                            <label for="email" class="block mb-1 text-sm font-medium text-gray-700">Email</label>
                            <input type="email" id="email" v-model="form.email"
                                   class="form-input w-full border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" />
                            <span class="text-red-800" v-if="errors.email">{{errors.email}}</span>
                        </div>
                        <div>
                            <label for="companyName" class="block mb-1 text-sm font-medium text-gray-700">Company Name</label>
                            <input type="text" id="companyName" v-model="form.companyName"
                                   class="form-input w-full border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" />
                            <span class="text-red-800" v-if="errors.companyName">{{errors.companyName}}</span>
                        </div>
                        <div>
                            <label for="website" class="block mb-1 text-sm font-medium text-gray-700">Website</label>
                            <input type="url" id="website" v-model="form.website"
                                   class="form-input w-full border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500"
                                   placeholder="https://example.com" />
                            <span class="text-red-800" v-if="errors.website">{{errors.website}}</span>
                        </div>
                    </div>
                    <div class="pt-4">
                        <button type="button" @click="goToNextStep()" class="w-full bg-blue-600 text-white py-2 rounded-md hover:bg-blue-700 transition">Next</button>
                    </div>
                </form>
            </div>


            <div v-if="step === 2" >
                <!-- Title and Description -->
                <div class="text-center mb-6">
                    <h2 class="text-2xl font-bold text-gray-800">Describe your website</h2>
                    <p class="text-gray-500 mt-2">Basic details about you and your business</p>
                </div>
                <!-- Step 2 -->
                <form class="space-y-4">
                    <div class="text-center mb-4">
                        <h3 class="text-lg font-semibold text-gray-800">Select Website Type</h3>
                    </div>
                    <div class="space-y-3">
                        <div v-for="websiteType of websiteTypes" :key="websiteType" class="flex items-center">
                            <input :id="`websiteType-${websiteType}`" type="radio" :value="websiteType" v-model="form.websiteType" name="type"
                                   class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500">
                            <label :for="`websiteType-${websiteType}`" class="ml-2 text-sm text-gray-700">{{websiteType}}</label>
                        </div>
                        <span class="text-red-800" v-if="errors.websiteType">{{errors.websiteType}}</span>
                    </div>

                    <div class="pt-6 flex justify-between">
                        <button @click="goBack()" type="button"
                                class="bg-gray-300 text-gray-700 py-2 px-4 rounded-md hover:bg-gray-400 transition">Back</button>
                        <button  type="button" @click="goToNextStep()"  class="bg-blue-600 text-white py-2 px-6 rounded-md hover:bg-blue-700 transition">Next</button>
                    </div>
                </form>
            </div>


            <div v-if="step === 3" >
                <!-- Title and Description -->
                <div class="text-center mb-6">
                    <h2 class="text-2xl font-bold text-gray-800">Describe your platform</h2>
                    <p class="text-gray-500 mt-2">Basic details about you and your business</p>
                </div>
                <!-- Step 2 -->
                <form class="space-y-4">
                    <div class="text-center mb-4">
                        <h3 class="text-lg font-semibold text-gray-800">Select Platform</h3>
                    </div>
                    <div class="space-y-3">
                        <div v-for="platformType of platformTypes" :key="platformType" class="flex items-center">
                            <input :id="`websiteType-${platformType}`" type="radio" :value="platformType" v-model="form.platform" name="type"
                                   class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500">
                            <label :for="`websiteType-${platformType}`" class="ml-2 text-sm text-gray-700">{{platformType}}</label>
                        </div>
                        <span class="text-red-800" v-if="errors.platform">{{errors.platform}}</span>
                    </div>

                    <div class="pt-6 flex justify-between">
                        <button @click="goBack()" type="button"
                                class="bg-gray-300 text-gray-700 py-2 px-4 rounded-md hover:bg-gray-400 transition">Back</button>
                        <button  type="button" @click="goToNextStep()"  class="bg-blue-600 text-white py-2 px-6 rounded-md hover:bg-blue-700 transition">Next</button>
                    </div>
                </form>
            </div>


            <div v-if="step === 4" >
                <!-- Title and Description -->
                <div class="text-center mb-6">
                    <h2 class="text-2xl font-bold text-gray-800">Review Your Details</h2>
                    <p class="text-gray-500 mt-2">Basic details about you and your business</p>
                </div>
                <!-- Step 2 -->
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
                    <button @click="goBack()" type="button"
                            class="bg-gray-300 text-gray-700 py-2 px-4 rounded-md hover:bg-gray-400 transition">Back</button>
                    <button  type="button" @click="submitForm()"  class="bg-blue-600 text-white py-2 px-6 rounded-md hover:bg-blue-700 transition">
                        Submit
                    </button>
                </div>
            </div>

            <Loader v-if="loading" />
            <Toast
                v-if="toastMessage"
                :type="toastType"
                :message="toastMessage"
                :duration="3000"
                @closed="toastMessage = ''"
            />

        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import * as yup from 'yup'
import apiClient from './../services/axios'
import Loader from './Loader.vue'
import Toast from './Toast.vue'

const step = ref(1);
const loading = ref(false);
const toastMessage = ref('')
const toastType = ref('success') // success | error | warning | info
function showToast(msg, type = 'success') {
    toastMessage.value = msg
    toastType.value = type
}
const steps = ['Basic Info', 'Website Details', 'Platform', 'Review & Submit']; // adjust as needed

const websiteTypes = ['E-commerce', 'Blog/Content Site', 'Corporate/Business Site', 'Portfolio', 'Other'];
const platformTypes = ref([]);

const step1Schema = yup.object({
    name: yup.string().required('Name is required'),
    email: yup.string().email('Invalid email').required('Email is required'),
    companyName: yup.string().required('Company Name is required'),
    website: yup.string().optional().url('Invalid Website URL'),
})

const step2Schema = yup.object({
    websiteType: yup.string().required('Website type is required'),
})

const step3Schema = yup.object({
    platform: yup.string().required('Platform is required'),
})

const form = ref({
    name: null,
    email: null,
    companyName: null,
    website: null,
    websiteType: null,
    platform: null
});

const errors = ref({
    name: null,
    email: null,
    companyName: null,
    website: null,
    websiteType: null,
    platform: null
});

function goBack() {
    if (step.value > 1) {
        step.value--;
    }
}

function goToNextStep() {
    if (step.value === 1) {
        step1Schema.validate(form.value, { abortEarly: false })
            .then(() => {
                goToNext();
            })
            .catch(err => {
                handleErrors(err)
            });
    } else if (step.value === 2) {
        step2Schema.validate(form.value, { abortEarly: false })
            .then(() => {
                loading.value = true;
                // get website type and go to next step
                apiClient.get('/api/platforms', {
                    params: { websiteType: form.value.websiteType }
                })
                .then(response => {
                    platformTypes.value = response.data.platforms || [];
                    goToNext();
                    loading.value = false;
                })
                .catch(err => {
                    handleErrors(err);
                    loading.value = false;
                });
            })
            .catch(err => {
                handleErrors(err)
            });
    } else if (step.value === 3) {
        step3Schema.validate(form.value, { abortEarly: false })
            .then(() => {
                goToNext();
            })
            .catch(err => {
                handleErrors(err)
            });
    }
}

function handleErrors(err) {
    const errorMap = {};
    err.inner.forEach(error => {
        if (error.path && !errorMap[error.path]) {
            errorMap[error.path] = error.message;
        }
    });
    errors.value = errorMap;
}

function goToNext() {
    step.value++;
}

function resetForm() {
    form.value = {
        name: '',
        email: '',
        companyName: '',
        website: '',
        websiteType: null,
        platform: null
    };
    errors.value = {};
    step.value = 1;
}

function submitForm() {
    apiClient.post('/api/lead', form.value)
        .then(response => {
            resetForm();
            showToast('We have received your data successfully!', 'success');
        })
        .catch(error => {
            showToast('Failed to submit form. Please try again later.', 'error');
        });
}

</script>