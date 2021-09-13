<template>
  <div class="home">
     <WelcomeLogo/>
    <BreedsGrid />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import WelcomeLogo from "@/components/WelcomeLogo.vue"; // @ is an alias to /src
import BreedsGrid from "@/components/BreedsGrid.vue"; // @ is an alias to /src

@Component({
  components: {
    WelcomeLogo,
    BreedsGrid,
  },
})
export default class Home extends Vue {}
</script>
