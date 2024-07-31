<script setup>
import gsap from 'gsap';
import Lenis from '@studio-freight/lenis';
import { onMounted } from 'vue';
import { ScrollTrigger } from 'gsap/all';

onMounted(() => {
    gsap.registerPlugin(ScrollTrigger);

    const lenis = new Lenis({
        lerp: .1,
        smoothWheel: true
    });

    lenis.on('scroll', ScrollTrigger.update);
    gsap.ticker.lagSmoothing(0);

    function raf(time) {
        lenis.raf(time);
        requestAnimationFrame(raf);
    }

    requestAnimationFrame(raf);
});
</script>


<template>
    <div class="pk__page">
        <main class="pk__page_content">
            <RouterView />
        </main>
        
    </div>
</template>


<style lang="scss">
@import "@/assets/_variables.scss";

.pk__page_content {
    background-color: $site-bg;
}

html.lenis, html.lenis body {
  height: auto;
}

.lenis.lenis-smooth {
  scroll-behavior: auto !important;
}

.lenis.lenis-smooth [data-lenis-prevent] {
  overscroll-behavior: contain;
}

.lenis.lenis-stopped {
  overflow: hidden;
}

.lenis.lenis-scrolling iframe {
  pointer-events: none;
}
</style>
