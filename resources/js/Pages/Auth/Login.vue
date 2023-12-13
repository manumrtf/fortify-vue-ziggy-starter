<template>
    <AuthLayout title="Login"
        description=" Lorem ipsum dolor sit amet consectetur adipisicing elit. Deserunt vitae temporibus sint quos maiores, harum explicabo.">
        <AuthForm :form="form" to="/login">
            <BaseInput v-model="form.email" name="email" label="Email" :errors="form.errors" required type="email" />

            <BaseInput v-model="form.password" name="password" label="Contraseña" :errors="form.errors" type="password"
                required />

            <input type="submit" value="Crear Cuenta"
                class="w-full bg-black text-white py-2 mt-2 rounded disabled:opacity-25" :disabled="form.processing" />
        </AuthForm>
    </AuthLayout>
</template>

<script setup>
import { useForm } from "@inertiajs/vue3";
import BaseInput from "@/Components/BaseInput.vue";
import AuthForm from "../../Components/AuthForm.vue";
import AuthLayout from "../../Layouts/AuthLayout.vue";
const form = useForm({
    email: null,
    password: null,
});
</script>
