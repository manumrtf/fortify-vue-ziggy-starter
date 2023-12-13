<template>
    <form class="w-full bg-white text-left flex flex-col gap-3 px-4 py-6" @submit.prevent="register()">
        <slot />
    </form>
</template>

<script setup>
const props = defineProps({
    to: String,
    form: Object
})

function register() {
    props.form.post(props.to, {
        preserveScroll: true,
        onSuccess: () => {
        },
        onError: (error) => {
            console.log(error);
        },

    });
}


</script>