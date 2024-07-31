<template>
    <section class="pk__small-text_section pk__section-margin-top pk__section-margin-bot">
        <div class="pk__container pk__m">
            <span class="pk__small-text_percent">15mins</span>
            <p>That's all it takes to get started! Schedule your 15 minute discovery call and together, we will begin the process to design and create something truly breathtaking for you and your family.</p>
            <Button href="#">Schedule Consultation</Button>
        </div>
    </section>
</template>

<script setup>
// Components
import Button from '@/components/Button.vue';

</script>

<style lang="scss">
@import "@/assets/_variables";

.pk__small-text_section {
    text-align: center;

    .pk__small-text_percent {
        font-size: 7rem;
        font-family: $heading-font-stack;
        line-height: 1;
        color: lighten($font-color, 70%);
    }

    p {
        font-weight: 300;
    }

    @media #{$l-and-up} {
        p {
            font-size: 1.4vw;
        }
    }
}
</style>