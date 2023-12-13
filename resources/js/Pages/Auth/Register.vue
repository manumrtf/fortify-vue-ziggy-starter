<template>
    <AuthLayout title="Register"
        description="  Lorem ipsum dolor sit amet consectetur adipisicing elit. Deserunt vitae temporibus sint quos maiores, harum explicabo.">
        <AuthForm :form="form" to="/register">
            <BaseInput v-model="form.name" name="name" label="Nombre" :errors="form.errors" required />

            <BaseInput v-model="form.email" name="email" label="Email" :errors="form.errors" type="email" required />

            <BaseInput v-model="form.password" name="password" label="Contraseña" :errors="form.errors" type="password"
                required minLength="8" />

            <BaseInput v-model="form.password_confirmation" name="password_confirmation" label="Confirmar Contraseña"
                :errors="form.errors" type="password" minLength="8" required />

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
    name: null,
    password: null,
    password_confirmation: null,
});
</script>
