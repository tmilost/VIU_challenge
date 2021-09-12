<template>
  <div class="hello">
    <div>
      <div class="container">
  <div class="photos">
    <img src="http://fakeimg.pl/360x360/000/?text=1">
    <img src="http://fakeimg.pl/360x360/111/?text=2">
    <img src="http://fakeimg.pl/360x360/222/?text=3">
    <img src="http://fakeimg.pl/360x360/333/?text=4">
    <img src="http://fakeimg.pl/360x360/444/?text=5">
    <img src="http://fakeimg.pl/360x360/555/?text=6">
    <img src="http://fakeimg.pl/360x360/666/?text=7">
    <img src="http://fakeimg.pl/360x360/777/?text=8">
    <img src="http://fakeimg.pl/360x360/888/?text=9">
    <img src="http://fakeimg.pl/360x360/999/?text=10">
    <img src="http://fakeimg.pl/360x360/aaa/?text=11">
    <img src="http://fakeimg.pl/360x360/bbb/?text=12">
  </div>
</div>

    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;

   mounted() {
    //do something
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
	max-width: 960px;
	margin: 0 auto;
}
.photos {
	display: flex;
	background-color: #000;
	flex-direction: row;
	flex-wrap: wrap;
	justify-content: flex-start;
	align-content: stretch;
	padding: 0;
	max-width: 980px;
	img {
		display: block;
		float: left;
		flex: 0 0 auto;
		background-color: #fff;
	}
}
@media screen and (min-width: 1024px) {
	.photos {
		img {
			width: calc(100%/6);
			height: calc(100%/6);
		}
	}
}
@media screen and (min-width: 769px) and (max-width: 1024px) {
	.photos {
		img {
			width: calc(100%/4);
			height: calc(100%/4);
		}
	}
}
@media screen and (min-width: 481px) and (max-width: 768px) {
	.photos {
		img {
			width: calc(100%/3);
			height: calc(100%/3);
		}
	}
}
@media screen and (min-width: 321px) and (max-width: 480px) {
	.photos {
		img {
			width: calc(100%/2);
			height: calc(100%/2);
		}
	}
}
@media screen and (max-width: 320px) {
	.photos {
		img {
			width: 100%;
			height: 100%;
		}
	}
}

</style>
