<template>
    <main class="text-center min-h-screen flex flex-col justify-center">
        <div class="max-w-lg mx-auto relative">

            <div class="max-w-lg mx-auto w-full bg-white shadow-md relative px-8 py-4 ">
                <h1 class="text-2xl font-bold md:text-3xl">{{ title }}</h1>
                <p class="max-w-md mx-auto mt-2">
                    {{ description }}
                </p>
                <slot />
            </div>
        </div>
    </main>
</template>

<script setup>
defineProps({
    title: String,
    description: String
})
</script>