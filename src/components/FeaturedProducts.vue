<script setup>
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/all';
import { onMounted, onUnmounted, ref } from 'vue';
import { RouterLink } from 'vue-router';

// Components
import Link from '@/components/Link.vue';

// Images
import image1 from '@/assets/portfolio-1.jpg';
import image2 from '@/assets/portfolio-2.jpg';
import image3 from '@/assets/portfolio-3.jpg';
import image4 from '@/assets/portfolio-4.jpg';
import image5 from '@/assets/portfolio-5.jpg';

// Ref's 
const featuredProductsSectionRef = ref(null);
const ctx = ref(null);

// On Component Mount
onMounted(() => {
    gsap.registerPlugin(ScrollTrigger);

    ctx.value = gsap.context(() => {
        gsap.set('.pk__featured-products_product-card', {
            opacity: 0,
            y: '40px'
        });
        gsap.to('.pk__featured-products_product-card', {
            duration: 2.4,
            opacity: 1,
            y: 0,
            stagger: 0.1,
            ease: 'power4.out',
            scrollTrigger: {
                trigger: featuredProductsSectionRef.value,
                start: 'top 80%',
            },
        });
    });
});

onUnmounted(() => {
    if (ctx.value) ctx.value.revert();
});
</script>


<template>
    <section ref="featuredProductsSectionRef" class="pk__featured-products_section pk__section-margin-top pk__section-margin-bot">
        <div class="pk__container pk__featured-products_heading">
            <h2>Portfolio</h2>
            <Link
                href="#"
                size="sm"
            >
                View All
            </Link>
        </div>
        <div class="pk__container pk__featured-products_grid">
            <RouterLink to="#" class="pk__featured-products_product-card">
                <div class="pk__featured-products_product-card-image">
                    <img 
                        :src="image1"
                    >
                </div>
                <!-- <div class="pk__featured-products_product-card-details">
                    <h3>Bisque Onbuhimo</h3>
                    <span>$198.00</span>
                </div> -->
            </RouterLink>
            <RouterLink to="#" class="pk__featured-products_product-card">
                <div class="pk__featured-products_product-card-image">
                    <img 
                        :src="image2"
                    >
                </div>
                <!-- <div class="pk__featured-products_product-card-details">
                    <h3>Bluff & Whiskey Leather Onbuhimo</h3>
                    <span>$340.00</span>
                </div> -->
            </RouterLink>
            <RouterLink to="#" class="pk__featured-products_product-card">
                <div class="pk__featured-products_product-card-image">
                    <img 
                        :src="image3"
                    >
                </div>
                <!-- <div class="pk__featured-products_product-card-details">
                    <h3>Shade Ring Sling</h3>
                    <span>$220.00</span>
                </div> -->
            </RouterLink>
            <RouterLink to="#" class="pk__featured-products_product-card">
                <div class="pk__featured-products_product-card-image">
                    <img 
                        :src="image4"
                    >
                </div>
                <!-- <div class="pk__featured-products_product-card-details">
                    <h3>Solstice & Honey Leath Onbuhimo</h3>
                    <span>$440.00</span>
                </div> -->
            </RouterLink>
            <RouterLink to="#" class="pk__featured-products_product-card">
                <div class="pk__featured-products_product-card-image">
                    <img 
                        :src="image5"
                    >
                </div>
                <!-- <div class="pk__featured-products_product-card-details">
                    <h3>Bisque Onbuhimo</h3>
                    <span></span>
                </div> -->
            </RouterLink>
        </div>
    </section>
</template>


<style lang="scss" scoped>
@import "@/assets/_variables";

.pk__featured-products_section {
    overflow: hidden;

    .pk__featured-products_heading {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 40px;

        h2 {
            text-transform: uppercase;
            font-size: .75rem;
            letter-spacing: .125rem;
            font-family: $font-stack;
            color: lighten($font-color, 40%);
            margin-bottom: 0;
        }
    }

    .pk__featured-products_grid {
        display: flex;
        flex-wrap: nowrap;
        gap: 1rem;

        .pk__featured-products_product-card {
            display: block;
            width: 66%;
            flex: none;
            text-decoration: none;
            color: lighten($font-color, 40%);
            transition: none;

            .pk__featured-products_product-card-image {
                aspect-ratio: 3 / 4;
                position: relative;
                overflow: hidden;
                border-radius: $border-radius;
                background-color: darken($site-bg, 5%);

                img {
                    width: 100%;
                    height: 100%;
                    object-fit: cover;
                    object-position: 50% 50%;
                }
            }

            .pk__featured-products_product-card-details {
                padding-top: 20px;
                padding-left: 20px;
                padding-right: 20px;
                text-align: center;

                h3 {
                    font-size: .875rem;
                    text-transform: uppercase;
                    letter-spacing: .125rem;
                    margin-bottom: .25rem;
                    font-family: $font-stack;
                    overflow: hidden;
                    white-space: nowrap;
                    text-overflow: ellipsis;
                }

                span {
                    font-size: .875rem;
                }
            }
        }
    }

    @media #{$m-and-up} {
        .pk__featured-products_grid {
            .pk__featured-products_product-card {
                width: 30%;
            }
        }
    }

    @media #{$l-and-up} {
        .pk__featured-products_grid {
            gap: 2rem;

            .pk__featured-products_product-card {
                width: 22%;
            }
        }
    }
}
</style>