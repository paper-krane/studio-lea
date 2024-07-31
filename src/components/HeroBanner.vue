<script setup>
import gsap from 'gsap';
import { ref, onMounted } from 'vue';
import { ScrollTrigger } from 'gsap/all';

// Components
import Button from '@/components/Button.vue';

// Image 
import heroImage from '@/assets/hero.jpg';

// Refs
const heroImageContainer = ref(null);
const heroImageWrapRef = ref(null);
const heroImageRef = ref(null);
const swipeRef = ref(null);
const scrollIndicatorRef = ref(null);
const buttonHovered = ref(false);
const ctx = ref(null);

const mouseLeaveHandler = () => {
    gsap.to(scrollIndicatorRef.value, {
        opacity: 0,
        duration: 1,
        ease: 'power4.out',
    });
};

const mouseMoveHandler = (e) => {
    const { clientX, clientY } = e;

    if (buttonHovered.value || window.innerWidth < 1280) {
        mouseLeaveHandler();
    } else {
        gsap.to(scrollIndicatorRef.value, {
            left: `${clientX}px`,
            top: `${clientY}px`,
            opacity: 1,
            duration: 1,
            ease: 'power4.out',
        });
    }
};

// On Mounted
onMounted(() => {
    gsap.registerPlugin(ScrollTrigger);

    // Context
    ctx.value = gsap.context(() => {
        const tl = gsap.timeline();

        // Initial Animation
        tl.set(heroImageWrapRef.value, {
            width: '60%',
            height: '40%',
        }).set(heroImageRef.value, {
            scale: 1.2,
            opacity: 1
        }).set(swipeRef.value, {
            width: 'calc(100% + 4px)',
        }).to(swipeRef.value, {
            duration: 1.4,
            width: 0,
            ease: 'power4.inOut',
        }).to(heroImageWrapRef.value, {
            duration: 1.2,
            delay: -.2,
            width: '100%',
            height: '100%',
            ease: 'power4.inOut',
        }).to(heroImageRef.value, {
            scale: 1,
            duration: 1.2,
            delay: -1.2,
            opacity: .4,
            ease: 'power4.inOut',
        });

        // Reveal Content
        gsap.from('.pk__hero_content-reveal', {
            y: '100%',
            opacity: 0,
            stagger: .125,
            duration: 1.6,
            ease: 'power4.out',
            delay: 2,
        })
        
        // Parallax Background Image
        gsap.to(heroImageWrapRef.value, {
            scrollTrigger: {
                trigger: heroImageContainer.value,
                start: 'top top',
                scrub: true,
            },
            scale: 1.5,
            y: '30%',
            ease: 'none',
        });
    });
});
</script>


<template>
    <section class="pk__hero_section pk__section-padding-bot" ref="heroImageContainer" @mousemove="mouseMoveHandler" @mouseleave="mouseLeaveHandler">
        <div class="pk__hero_image" ref="heroImageWrapRef">
            <div class="pk__hero_image-container">
                <img 
                    ref="heroImageRef"
                    :src="heroImage" 
                    alt="Hero Image" 
                />
            </div>
            <div class="pk__hero_swipe-cover" ref="swipeRef"></div>
        </div>
        <div class="pk__hero_content">
            <div class="pk__container">
                <h1>
                    <div class="pk__hero_overflow-hidden">
                        <span class="pk__heading-accent pk__hero_content-reveal">Denver Interior Design </span>
                    </div>
                    <div class="pk__hero_overflow-hidden">
                        <span class="pk__hero_content-reveal">Creating beautiful & functional interiors for </span>
                    </div>
                    <div class="pk__hero_overflow-hidden">
                        <span class="pk__hero_content-reveal"><span class="pk__text-italic">your</span> dream space</span>
                    </div>
                </h1>
                <div class="pk__hero_overflow-hidden">
                    <span class="pk__hero_content-reveal" @mouseenter="buttonHovered = true" @mouseleave="buttonHovered = false">
                        <Button href="#">Let's Talk...</Button>
                    </span>
                </div>
            </div>
        </div>
        <div class="pk__hero_scroll-indicator" ref="scrollIndicatorRef">
            Scroll
        </div>
    </section>
</template>


<style lang="scss">
@import "@/assets/_variables";

.pk__hero_section {
    position: relative;
    width: 100%;
    height: 100svh;
    overflow: hidden;
    display: flex;
    align-items: flex-end;

    .pk__hero_image, .pk__hero_image-container {
        position: absolute;
        top: 50%;
        left: 50%;
        width: 100%;
        height: 100%;
        transform: translate(-50%, -50%);

        .pk__hero_swipe-cover {
            position: absolute;
            top: -2px;
            right: -2px;
            height: calc(100% + 4px);
            background-color: $site-bg;
        }
    }

    .pk__hero_image {
        .pk__hero_swipe-cover {
            position: absolute;
            top: -2px;
            right: -2px;
            height: calc(100% + 4px);
            background-color: $site-bg;
        }
    }

    .pk__hero_image-container {
        overflow: hidden;
        background-color: $font-color;

        img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            object-position: 50% 80%;
            opacity: .4;
        }
    }

    .pk__hero_content {
        position: relative;
        color: $white;
        width: 100%;
        flex: none;

        h1 {
            font-size: 6vw;
        }

        .pk__hero_overflow-hidden {
            overflow: hidden;
        }

        .pk__hero_content-reveal {
            display: inline-block;
            position: relative;
        }

        .pk__text-italic {
            position: relative;

            &:before {
                content: '';
                position: absolute;
                top: 50%;
                right: calc(100% + 16px);
                width: 100%;
                height: 1px;
                background-color: $white;
                transform: translateY(-50%);
            }
        }
    }

    .pk__hero_scroll-indicator {
        display: none;
    }

    @media #{$m-and-up} {
        .pk__hero_content {
            text-align: right;

            h1 {
                font-size: 2.25rem;
            }
        }
    }

    @media #{$l-and-up} {
        .pk__hero_content {
            h1 {
                font-size: 3.5rem;
            }
        }

        .pk__hero_scroll-indicator {
            position: fixed;
            z-index: 2;
            font-size: .825rem;
            color: $white;
            backdrop-filter: blur(6px);
            -webkit-backdrop-filter: blur(6px);
            display: flex;
            align-items: center;
            justify-content: center;
            width: 64px;
            height: 64px;
            border-radius: 50%;
            opacity: 0;
            pointer-events: none;
        }
    }
}
</style>