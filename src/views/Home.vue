<template>
  <div class="home">
    <BreedsGrid msg="Welcome to Your Vue.js + TypeScript App" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import BreedsGrid from "@/components/BreedsGrid.vue"; // @ is an alias to /src

@Component({
  components: {
    BreedsGrid,
  },
})
export default class Home extends Vue {}
</script>
