<template>
    <nav class="bg-white shadow">
        <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
            <div class="relative flex h-16 items-center justify-between">
                <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
                    <!-- Mobile menu button-->
                    <button type="button"
                        class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white"
                        aria-controls="mobile-menu" aria-expanded="false" @click="isMobileMenuOpen = !isMobileMenuOpen">
                        <span class="absolute -inset-0.5"></span>
                        <span class="sr-only">Open main menu</span>
                        <!--
            Icon when menu is closed.

          -->
                        <svg v-if="!isMobileMenuOpen" class="block h-6 w-6" fill="none" viewBox="0 0 24 24"
                            stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
                        </svg>
                        <!--
            Icon when menu is open.

          -->
                        <svg v-if="isMobileMenuOpen" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                            stroke="currentColor" aria-hidden="true">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </button>
                </div>
                <div class="flex flex-1 items-center justify-center ">
                    <div class="flex flex-shrink-0 items-center">
                        <img class="h-8 w-auto" src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=500"
                            alt="Your Company" />
                    </div>
                    <div class="hidden sm:ml-6 sm:block">
                        <div class="flex space-x-4">
                            <!--
                            when pathName is home, we will send the hardcoded URL
                            this is to avoid route function to convert it to something
                            like 127.0.0.1:8000 that will make it harder to track
                            if we are on the homepage
                            -->
                            <NavigationLink v-for="link in links" :href="link.pathName === 'home'
                                ? '/'
                                : route(link.pathName)
                                ">
                                {{ link.name }}
                            </NavigationLink>
                        </div>
                    </div>
                </div>
                <div class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0">
                    <!-- Profile dropdown -->
                    <div v-if="user" class="relative ml-3">
                        <div>
                            <button type="button"
                                class="relative flex rounded-full bg-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800"
                                id="user-menu-button" aria-expanded="false" aria-haspopup="true"
                                @click="isUserPanelOpen = !isUserPanelOpen">
                                <span class="absolute -inset-1.5"></span>
                                <span class="sr-only">Open user menu</span>
                                <img class="h-8 w-8 rounded-full"
                                    src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                                    alt="" />
                            </button>
                        </div>

                        <!--
            Dropdown menu, show/hide based on menu state.

            Entering: "transition ease-out duration-100"
              From: "transform opacity-0 scale-95"
              To: "transform opacity-100 scale-100"
            Leaving: "transition ease-in duration-75"
              From: "transform opacity-100 scale-100"
              To: "transform opacity-0 scale-95"
          -->
                        <div v-show="isUserPanelOpen"
                            class="absolute right-0 z-10 mt-2 w-48 origin-top-right rounded-md bg-white py-1 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
                            role="menu" aria-orientation="vertical" aria-labelledby="user-menu-button" tabindex="-1">
                            <!-- Active: "bg-gray-100", Not Active: "" -->
                            <Link v-for="link in userDropDownLinks" :href="route(link.pathName)"
                                class="block px-4 py-2 text-sm text-gray-700" role="menuitem" tabindex="-1"
                                id="user-menu-item-0">{{ link.name }}</Link>
                            <button class="block px-4 py-2 text-sm text-gray-700" @click="logOut">
                                Cerrar Sesión
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Mobile menu, show/hide based on menu state. -->
        <div v-if="isMobileMenuOpen" class="sm:hidden" id="mobile-menu">
            <div class="space-y-1 px-2 pb-3 pt-2">
                <!--
                    when pathName is home, we will send the hardcoded URL
                    this is to avoid route function to convert it to something
                    like 127.0.0.1:8000 that will make it harder to track
                    if we are on the homepage
                -->
                <NavigationLink v-for="link in links" :href="link.pathName === 'home' ? '/' : route(link.pathName)
                    " target="mobile">
                    {{ link.name }}
                </NavigationLink>
            </div>
        </div>
    </nav>
</template>

<script setup>
import { ref, computed, watch } from "vue";
import { Link, useForm, usePage } from "@inertiajs/vue3";
import NavigationLink from "./NavigationLink.vue";

const page = usePage();

const isUserPanelOpen = ref(false);

const isMobileMenuOpen = ref(false);
const user = ref(page.props.auth.user);
const baseLinks = [
    {
        name: "Inicio",
        pathName: "home",
    },
];

function authLinks(user) {
    if (!user) {
        return [
            {
                name: "Iniciar Sesión",
                pathName: "login",
            },
            {
                name: "Registrarse",
                pathName: "register",
            },
        ];
    }

    return [];
}

const links = ref([...baseLinks, ...authLinks(user.value)]);

const userDropDownLinks = [
    {
        name: "Ajustes",
        pathName: "settings",
    },
];

const form = useForm({});
function logOut() {
    form.post("/logout");
}

// Use a watch effect to update the user when it changes in the page props
watch(
    () => page.props.auth.user,
    (newUser) => {
        links.value = [...baseLinks, ...authLinks(newUser?.value ?? false)];
        user.value = newUser
    }
);
</script>
