<template>
<div id="game">
    <background/>
    <intro/>
    <hack-game v-if="$store.getters.isPlaying"/>
    <outro v-if="!$store.getters.isPlaying"/>
</div>
</template>


<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Background from "@/components/Game/Background.vue";
import Intro from "@/components/Game/Intro.vue";
import HackGame from "@/components/Game/HackGame.vue";
import Guess from "@/classes/Guess.ts";
import Outro from "@/components/Game/Outro.vue";
import GameManager from "@/classes/GameManager.ts";
import Config from "@/classes/Config.ts";

@Component({
    components: {
        Background, Intro, HackGame, Outro
    }
})
export default class Game extends Vue {
    public created() {
        // Reset game state whenever page is visited
        GameManager.generateCode(Config.DIGIT_COUNT);
        this.$store.commit("resetGame");
        this.$store.commit("setCorrectCode", GameManager.digitArray.join(""));
        Guess.resetAutoIncrementId();
    }
}
</script>

<style lang="scss">
#game {
    color: #6090d7;
}
</style>
