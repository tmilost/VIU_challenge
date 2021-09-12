<template>
  <div class="hello">
    <div>
      <div class="image-grid">
        <div class="grid-image" v-for="(breed,index) in RandomImageBreeds" :key="breed">
          <img
            style="width: 250px; height: 170px"
            class="centered project-image-bg"
            :src="breed"
            alt=""
          />
          <button
            class="
              uppercase
              viu-button viu-button--secondary
              viu-buttons-list__list-item
            "
          >
           {{allBreeds[index]}} 
          </button>
        </div>
      </div>

      <!-- /////////////////////// -->
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import axios from "axios";

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;

  private allBreeds: string[] = [];
  private RandomImageBreeds: string[] = [];

  public async getAllBreeds() {
    const { data } = await axios.get("https://dog.ceo/api/breeds/list/all");

    for (let breed in data.message) {
      this.allBreeds.push(breed);
    }
	this.getRandomImageBreed()
    ////////////////////////////////
 
  }

  public async getRandomImageBreed() {
      this.allBreeds.forEach((breed) => {
      axios
        .get("https://dog.ceo/api/breed/" + breed + "/images/random")
        .then((response) => {
          this.RandomImageBreeds.push(response.data.message);
  
        })
        .catch((e) => {
          console.log(e);
        });
    });
  }

  //  public getRandomImageBreed() {
  //  var ss:string;
  //   axios.get("https://dog.ceo/api/breed/hound/images/random").then((response) => {
  //       ss = response.data.message;
  //         console.log(response.data.message);

  //       })
  //       .catch((e) => {
  //         console.log(e);
  //       });
  //  return "https://images.dog.ceo/breeds/hound-afghan/n02088094_5345.jpg";

  //   }

  mounted() {
    this.getAllBreeds();

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
//////////////////////////////
.image-grid {
  justify-content: center;
  /* Arrange children using flexbox */
  display: flex;
  /* ALlow images to display on multiple lines rather than a single line */
  flex-wrap: wrap;
  /* Container should take up only 90% of the browser, leave 5% space on each side */
  max-width: 960px;
  /* Center container */
  margin: 0 auto;
}
.grid-image {
  /* images display inline by default and act like text. We want them to act like divs, so display block */
  display: block;
  /* our width setting for mobile, one image per line */
  flex-basis: 100%;
  /* provide some space between our images */
  padding: 10px;
  /* ensure padding doesn't cause images to wrap, it should be within the width rather than in addition */
  box-sizing: border-box;
}

/* increase images per line as browser gets larger using media queries
   this first query makes two images per line at 640px width */
@media only screen and (min-width: 640px) {
  .grid-image {
    flex-basis: 50%;
  }
}

/* three images per line when browser width exceeds 960px */
@media only screen and (min-width: 960px) {
  .grid-image {
    flex-basis: 33.333%;
  }
}

/* four images per line when browser width exceeds 1280px */
@media only screen and (min-width: 1280px) {
  .grid-image {
    flex-basis: 25%;
  }
}

/* five images per line when browser width exceeds 1600px */
@media only screen and (min-width: 1600px) {
  .grid-image {
    flex-basis: 20%;
  }
}

/////////////////////////////////////////


.viu-button--secondary:hover {
  background: #000;
  border-color: #000;
  color: #fff;
}
.viu-button {
  font-family: europa, sans-serif;
  background: transparent;
  border: 1px solid #000;
  color: #000;
  align-items: center;
  cursor: pointer;
//   display: flex;
  
  flex-basis: auto;
  flex-direction: column;
  flex-grow: 0;
  flex-shrink: 0;
  max-height: 48px;
  min-height: 48px;
  justify-content: center;
  padding: 1px 15px;
  text-align: center;
  width: 250px;
  padding-top: 1em;
}
</style>
