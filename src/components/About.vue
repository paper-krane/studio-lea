<script setup>
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/all';
import { computed, onMounted, onUnmounted, ref } from 'vue';

// Components
import Button from '@/components/Button.vue';

// Images
import image1 from '@/assets/about-1.jpg';
import image2 from '@/assets/about-2.jpg';

// Ref's
const words = computed(() => {
    const paraStr = 'We are a full-service interior design firm. From custom new build residences to furnishing selections and design consultations, we are dedicated to helping you transform your space into something incredibly beautiful and functional.';
    const paraArr = paraStr.split(' ');

    return paraArr;
})
const aboutImageRef = ref(null);
const aboutImageWrapRef = ref(null);
const aboutImage2Ref = ref(null);
const aboutImageWrap2Ref = ref(null);
const aboutContentRef = ref(null);
const ctx = ref(null);

// On Component Mount
onMounted(() => {
    gsap.registerPlugin(ScrollTrigger);

    ctx.value = gsap.context(() => {
        gsap.to(aboutImageRef.value, {
            y: '10vh',
            ease: 'linear',
            scrollTrigger: {
                trigger: aboutImageWrapRef.value,
                scrub: 0.2,
                invalidateOnRefresh: true,
            },
        
        });
        gsap.to(aboutImage2Ref.value, {
            y: '10vh',
            ease: 'linear',
            scrollTrigger: {
                trigger: aboutImageWrap2Ref.value,
                scrub: 0.2,
                invalidateOnRefresh: true,
            },
        
        });

        gsap.to('.pk__about_content-container > p > span', {
            backgroundPositionX: '0%',
            ease: 'linear',
            stagger: 0.6,
            scrollTrigger: {
                trigger: aboutContentRef.value,
                scrub: 0.2,
                invalidateOnRefresh: true,
                end: 'bottom 40%'
            },
        });
    });
})
</script>


<template>
    <section class="pk__about_section pk__section-margin-top pk__section-margin-bot">
        <div class="pk__container">
            <div class="pk__about_image-container">
                <div class="pk__about_image-wrap" ref="aboutImageWrapRef">
                    <figure class="pk__about_image" ref="aboutImageRef">
                        <img :src="image1" style="object-position: 50% 70%;" loading="lazy">
                    </figure>
                </div>
                <div class="pk__about_image-wrap wrap-2" ref="aboutImageWrap2Ref">
                    <figure class="pk__about_image" ref="aboutImage2Ref">
                        <img :src="image2" style="object-position: 50% 30%;" loading="lazy">
                    </figure>
                </div>
            </div>
            <div class="pk__about_content-container">
                <h3>We take pride in our work.</h3>
                <p ref="aboutContentRef">
                    <span v-for="(word, index) in words" :key="`${word}-${index}`">{{ word }} </span>
                </p>
                <Button href="#">
                    Meet Our Team
                </Button>
            </div>
        </div>
    </section>
</template>


<style lang="scss">
@import "@/assets/_variables";

.pk__about_section {
    .pk__about_image-container {
        margin-bottom: 80px;
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 2rem;

        .pk__about_image-wrap {
            position: relative;
            aspect-ratio: 1 / 1;
            grid-column: span 2;
            overflow: hidden;
            border-radius: $border-radius;

            .pk__about_image {
                position: absolute;
                bottom: 0;
                left: 0;
                width: 100%;
                height: calc(100% + 10vh);
                margin: 0;

                img {
                    width: 100%;
                    height: 100%;
                    object-fit: cover;
                    object-position: 40% 0%;
                }
            }

            &.wrap-2 {
                grid-column: span 1;
                aspect-ratio: initial;

                .pk__about_image {
                    img {
                        object-position: 30% 0%;
                    }
                }
            }
        }
    }

    .pk__about_content-container {
        p {
            font-size: 1.25rem;
            font-weight: 300;

            span {
                display: inline-flex;
                margin-right: 4px;
                background-image: linear-gradient(to right, #{lighten($font-color, 10%)} 33%, #{lighten($font-color, 70%)} 66%);
                background-size: 300% 100%;
                background-position-x: 100%;
                color: transparent;
                background-clip: text;
                -webkit-background-clip: text;
            }
        }
    }

    @media #{$xl-and-up} {
        .pk__about_content-container {
            h3 {
                font-size: 2.75vw;
            }
        }
    }

    @media #{$xl-and-up} {
        .pk__container {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 80px;
            align-items: center;
        }

        .pk__about_image-container {
            margin-bottom: 0;
        }

        .pk__about_content-container {
            p {
                font-size: 1.5vw;

                span {
                    margin-right: .3vw;
                }
            }
        }
    }
}
</style>