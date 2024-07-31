<script setup>
import { RouterLink } from 'vue-router';

const props = defineProps({
    href: {type: String}, 
    target: {type: String},
    rel: {type: String, required: false},
    type: {type: String, default: 'button'}, 
    variant: {type: String, default: 'default'}, 
    class: {type: String, required: false},
    loading: {type: Boolean}, 
    disabled: {type: Boolean},
    eventHandler: {type: Function, required: false, default: null},
});
</script>


<template>
    <template v-if="props.href && !props.eventHandler">
        <RouterLink 
            ref="buttonRef"
            :to="props.href" 
            :target="props.target"
            class="pk__btn" 
            :class="`${props.variant} ${props.class}`" 
            :data-loading="props.loading ? 'true' : 'false'" 
            :data-disabled="props.disabled ? 'true' : 'false'"
            :rel="props.rel ? props.rel : null"
        >
            <span class="hf__btn-text">
                <slot />
            </span>
        </RouterLink>
    </template>
    <template v-else>
        <button
            ref="buttonRef"
            class="pk__btn" 
            :class="props.variant" 
            :type="props.type" 
            :data-loading="props.loading ? 'true' : 'false'" 
            :disabled="props.disabled ? 'true' : null"
            @[clickCondition].prevent="props.eventHandler"
            @[keyupCondition].enter.prevent="props.eventHandler"
        >
            <span class="pk__btn_text" :class="{'pk__btn_loading': buttonIsLoading}">
                <slot />
            </span>
            <span class="pk__btn_loading-spinner" v-if="buttonIsLoading"></span>
        </button>
    </template>
</template>


<style lang="scss">
@import "@/assets/_variables";

// Reset Styles
.pk__btn {
    text-decoration: none;
    position: relative;
    font-weight: inherit;
    border: none;
    border-radius: $border-radius;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-width: 40px;
    height: 56px;
    line-height: 56px;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    outline: none;
	z-index: 0;
    -webkit-tap-highlight-color: transparent;
	-webkit-backface-visibility: hidden;
    backface-visibility: hidden;
	-moz-osx-font-smoothing: grayscale;
}

// Button Styles
.pk__btn, .pk__btn:visited {
    background-color: $primary-color;
    font-size: .875rem;
    letter-spacing: .125rem;
    text-transform: uppercase;
    padding-right: 2rem;
    padding-left: 2rem;
    color: $white;
    transition: $transition-all;
}

.pk__btn:hover, .pk__btn:focus {
    background-color: $primary-accent-color;
    color: $white;
}
</style>