<template>
    <Link v-if="target === 'desktop'" v-bind="$attrs" class="rounded-md px-3 py-2 text-sm font-medium" :class="(route().current() === linkRoute ||
            (route().current() == 'home' && linkRoute === '/')) &&
        'text-pink-600 underline underline-offset-8'
        ">
    <slot />
    </Link>
    <Link v-if="target === 'mobile'" v-bind="$attrs" class="text-black block rounded-md px-3 py-2 text-base font-medium"
        :class="(route().current() === linkRoute ||
                (route().current() == 'home' && linkRoute === '/')) &&
            'bg-gray-800 text-white'
            ">
    <slot />
    </Link>
</template>

<script setup>
defineProps({
    target: {
        type: String,
        default: "desktop",
    },
});
import { Link, usePage } from "@inertiajs/vue3";
import { ref, useAttrs, computed } from "vue";
const { href } = useAttrs();
/*
    except when the route passed as prop is the root of our app
    that was sent hardcoded (check navigation component)
    we will stay only with the pathname to compare with the active route
 */
const linkRoute = href !== "/" ? ref(href.split("/").at(-1)) : "/";

const { url } = usePage().props;

// const isHome =
</script>
