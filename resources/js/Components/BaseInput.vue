<template>
    <div>
        <p class="text-red-600" v-if="errors[$attrs.name]">
            {{ errors[$attrs.name] }}
        </p>
        <label>{{ label }}</label>
        <input v-bind="$attrs" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"
            class="w-full rounded mt-2 shadow border-zinc-300" />
    </div>
</template>

<script setup>
defineProps({
    errors: Object,
    label: String,
    modelValue: String,
});

defineEmits(["update:modelValue"]);

defineOptions({
    inheritAttrs: false,
});
</script>
