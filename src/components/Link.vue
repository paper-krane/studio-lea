<script setup>
import { RouterLink } from 'vue-router';

const props = defineProps({
    href: { type: String, required: true },
    target: { type: String, default: '_self' },
    rel: { type: String },
    size: { type: String, enum: ['sm', 'md', 'lg'], default: 'md' },
});
</script>


<template>
    <RouterLink
        :to="href"
        :target="target"
        :rel="rel"
        class="pk__link"
        :class="size"
    >
        <slot />
        <span class="pk__link_underline"></span>
    </RouterLink>
</template>


<style lang="scss">
@import "@/assets/_variables";

.pk__link, .pk__link:visited {
    font-family: $font-stack;
    color: lighten($font-color, 40%);
    text-transform: uppercase;
    letter-spacing: .125rem;
    text-decoration: none;
    display: inline-block;
    white-space: nowrap;

    &.sm {
        font-size: .75rem;
        letter-spacing: .125rem;
    }

    .pk__link_underline {
        display: block;
        width: 100%;
        height: 2px;
        background-color: $font-color;
        transform: scaleX(0);
        transform-origin: 100% 50%;
        transition: transform .3s;
    }
}

.pk__link:hover, .pk__link:focus {
    color: $font-color;

    .pk__link_underline {
        transform: scaleX(1);
        transform-origin: 0 50%;
        transition: transform .3s;
    }
}
</style>