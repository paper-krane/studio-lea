<script setup>
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/all';
import { ref, onMounted } from 'vue';

// Images
import image1 from '@/assets/ticker-1.jpg';
import image2 from '@/assets/ticker-2.jpg';
import image3 from '@/assets/ticker-3.jpg';
import image4 from '@/assets/ticker-4.jpg';

// Ref's
const galleryEl = ref(null);
const gallerySection = ref(null);

// Example

// On Component Mount
onMounted(() => {
    const gallery = gsap.to(galleryEl.value, {
        duration: 60,
        ease: "none",
        x: `-100%`,
        repeat: -1,
    });

    ScrollTrigger.create({
        trigger: gallerySection.value,
        onUpdate(self) {
            const velocity = self.getVelocity();
            if (velocity < 0) return;
            const timeScale = 3 + (velocity / 100);
            gsap.timeline()
                .to(gallery, { duration: 0.25, timeScale })
                .to(gallery, { duration: .5, timeScale: 1 });
        }
    });
});
</script>


<template>
    <section class="pk__image-ticker_section pk__section-margin-top pk__section-margin-bot" ref="gallerySection">
        <div class="pk__container pk__image-ticker_header">
            <h5>Follow us on Instagram</h5>
            <a href="https://www.instagram.com/studioleainteriors/" target="_blank">
                @studioleainteriors
            </a>
        </div>
        <div class="pk__image-ticker_container" ref="galleryEl">
            <div class="pk__image-ticker">
                <div class="pk__image-ticker_item">
                    <div class="pk__image-ticker_image">
                        <figure>
                            <img :src="image1" alt="Placeholder image" />
                        </figure>
                    </div>
                </div>
                <div class="pk__image-ticker_item large">
                    <div class="pk__image-ticker_image">
                        <figure>
                            <img :src="image2" alt="Placeholder image" />
                        </figure>
                    </div>
                </div>
                <div class="pk__image-ticker_item">
                    <div class="pk__image-ticker_image">
                        <figure>
                            <img :src="image3" alt="Placeholder image" style="object-position: 80% 50%;" />
                        </figure>
                    </div>
                </div>
                <div class="pk__image-ticker_item small">
                    <div class="pk__image-ticker_image">
                        <figure>
                            <img :src="image4" alt="Placeholder image" />
                        </figure>
                    </div>
                </div>
                <div class="pk__image-ticker_item">
                    <div class="pk__image-ticker_image">
                        <figure>
                            <img :src="image1" alt="Placeholder image" />
                        </figure>
                    </div>
                </div>
                <div class="pk__image-ticker_item large">
                    <div class="pk__image-ticker_image">
                        <figure>
                            <img :src="image2" alt="Placeholder image" />
                        </figure>
                    </div>
                </div>
                <div class="pk__image-ticker_item">
                    <div class="pk__image-ticker_image">
                        <figure>
                            <img :src="image3" alt="Placeholder image" style="object-position: 80% 50%;" />
                        </figure>
                    </div>
                </div>
                <div class="pk__image-ticker_item small">
                    <div class="pk__image-ticker_image">
                        <figure>
                            <img :src="image4" alt="Placeholder image" />
                        </figure>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>


<style lang="scss">
@import "@/assets/_variables";

.pk__image-ticker_section {
    overflow: hidden;

    .pk__image-ticker_header {
        margin-bottom: 40px;
        display: flex;
        justify-content: space-between;
        align-items: center;

        h5 {
            margin-bottom: 0;
        }

        a, a:visited {
            font-size: .825rem;
            color: lighten($font-color, 40%);
            font-style: italic;
            text-decoration: none;
        }
    }

    .pk__image-ticker_container {
        position: relative;
    }

    .pk__image-ticker {
        position: relative;
        display: inline-flex;
        align-items: center;
    }

    .pk__image-ticker_item {
        width: 23.33333333337vw;
        padding: 0 10px;
        flex-grow: 0;
        flex-shrink: 0;
        position: relative;

        &.large {
            width: 30vw;
        }

        &.small {
            .pk__image-ticker_image {
                aspect-ratio: 3 / 2;
            }
        }

        .pk__image-ticker_image {
            position: relative;
            overflow: hidden;
            border-radius: $border-radius;
            aspect-ratio: 2 / 3;

            figure {
                position: absolute;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;

                img {
                    width: 100%;
                    height: 100%;
                    object-fit: cover;
                    object-position: 50% 50%;
                }
            }
        }
    }

    @media #{$l-and-up} {
        .pk__image-ticker_item {
            padding: 0 16px;
        }
    }
}
</style>