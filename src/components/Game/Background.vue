<template>
<div class="background">
    <div class="bg-color"></div>
    <div class="badge inner" v-if="isPlaying"></div>
    <div class="badge outer"></div>
</div>
</template>

<script lang="ts">
import {Component, Vue} from "vue-property-decorator";

@Component
export default class Background extends Vue {
    protected get isPlaying(): boolean {
        return this.$store.getters.isPlaying;
    }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/styles/Body.scss";
@import "@/styles/Game.scss";
@import "@/styles/Graphic.scss";
$image-folder: "../../assets/image";
$badge-inner-initial-scale: 0.125;

.background {
    > div {
        @include graphic();
    }
}
.bg-color {
    width: $game-width;
    height: $game-height;
    background-image: url("#{$image-folder}/Background.webp");
    background-size: contain;
    background-repeat: no-repeat;
    border-radius: 16px;
}
.badge {
    top: 156px;
    width: 336px;
    height: 318px;
    background-image: url("#{$image-folder}/HKPDLogoMask.webp");
    background-size: contain;
    background-repeat: no-repeat;
    mix-blend-mode: color-dodge;
    visibility: hidden;
    &.inner {
        animation-delay: 1s;
        animation-duration: 1s;
        animation-name: badge-inner-fade-in;
        animation-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
        animation-fill-mode: forwards;
        transform: scale(#{$badge-inner-initial-scale});
        filter: brightness(0);
    }
    &.outer {
        animation-delay: 0.5s;
        animation-duration: 1.5s;
        animation-name: badge-outer-fade-in-out;
        animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1);
        animation-fill-mode: forwards;
        filter: blur(0px) brightness(0);
    }
    &:empty {
        display: block;
    }
}
@keyframes badge-inner-fade-in {
    from {
        transform: scale(#{$badge-inner-initial-scale});
        filter: brightness(0);
        visibility: visible;
    }
    to {
        transform: scale(1);
        filter: brightness(1);
        visibility: visible;
    }
}
@keyframes badge-outer-fade-in-out {
    0% {
        filter: blur(0px) brightness(0);
        visibility: visible;
    }
    22% {
        filter: blur(1px) brightness(1.25);
    }
    33% {
        filter: blur(5px) brightness(100);
    }
    55% {
        filter: blur(7px) brightness(4);
    }
    100% {
        filter: blur(3px) brightness(0);
        visibility: hidden;
    }
}
</style>
