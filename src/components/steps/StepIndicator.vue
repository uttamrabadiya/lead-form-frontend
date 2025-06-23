<!-- StepIndicator.vue -->
<template>
    <div class="flex justify-between items-center mb-8">
        <div
            v-for="(label, index) in steps"
            :key="index"
            class="flex-1 flex flex-col items-center gap-2 text-center relative"
        >
            <!-- Step circle -->
            <div
                class="flex items-center justify-center w-8 h-8 rounded-full text-white text-sm font-medium z-10"
                :class="{
          'bg-blue-600': currentStep > index,
          'bg-blue-500': currentStep === index + 1,
          'bg-gray-300': currentStep < index + 1
        }"
            >
                {{ index + 1 }}
            </div>

            <!-- Step label -->
            <p
                class="text-sm font-medium"
                :class="{
          'text-blue-600': currentStep >= index + 1,
          'text-gray-400': currentStep < index + 1
        }"
            >
                {{ label }}
            </p>

            <!-- Connecting line -->
            <div
                v-if="index !== steps.length - 1"
                class="absolute top-4 right-0 w-full h-0.5 z-0"
                :class="{
          'bg-blue-600': currentStep > index + 1,
          'bg-gray-300': currentStep <= index + 1
        }"
                style="z-index: -1; transform: translateX(50%); width: 100%"
            ></div>
        </div>
    </div>
</template>

<script setup>
defineProps({
    steps: Array,
    currentStep: Number
})
</script>
