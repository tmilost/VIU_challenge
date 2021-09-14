<template>
  <div class="home">
    <WelcomeLogo />
    <BreedsGrid />
    <SausageDog />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import WelcomeLogo from "@/components/WelcomeLogo.vue";
import BreedsGrid from "@/components/BreedsGrid.vue";
import SausageDog from "@/components/SausageDog.vue";

@Component({
  components: {
    WelcomeLogo,
    BreedsGrid,
    SausageDog,
  },
})
export default class Home extends Vue {}
</script>
