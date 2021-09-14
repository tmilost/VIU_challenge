<template>
  <div class="hello">
    <div>
      <div class="per-page-pagination">
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          background
          :page-sizes="[5, 10, 15]"
          :page-size="this.pageSize"
          layout="total ,sizes"
          :total="this.RandomImageBreeds.length"
        >
        </el-pagination>
      </div>
      <div class="image-grid">
        <div
          class="grid-image"
          v-for="(breed, index) in allBreedsFiltered"
          :key="index"
        >
          <el-image
            class="centered project-image-bg el-image-component"
            :alt="breed"
            lazy
            :src="allBreedWithRandomImage[breed]"
            :preview-src-list="[...allBreedWithRandomImage[breed]]"
          >
          </el-image>

          <button
            class="
              uppercase
              viu-button viu-button--secondary
              viu-buttons-list__list-item
            "
          >
            {{ breed }}
          </button>
        </div>
      </div>
    </div>
    <div class="page-pagination">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        background
        :page-sizes="[5, 10, 15]"
        :page-size="this.pageSize"
        layout=" prev, pager, next"
        :total="this.RandomImageBreeds.length"
      >
      </el-pagination>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import axios from "axios";

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;

  private allBreedWithRandomImage: { [key: string]: number } = {};
  private allBreeds: string[] = [];
  private RandomImageBreeds: string[] = [];
  private pageSize = 10;
  private pageNumber = 1;
  private allBreedsFiltered: string[] = [];
  private RandomImageBreedsFiltered: string[] = [];

  public async getAllBreeds() {
    const { data } = await axios.get("https://dog.ceo/api/breeds/list/all");

    for (let breed in data.message) {
      this.allBreeds.push(breed);
    }
    this.getRandomImageBreed();

    this.handleCurrentChange(1);
  }

  public async getRandomImageBreed() {
    this.allBreeds.forEach((breed) => {
      axios
        .get("https://dog.ceo/api/breed/" + breed + "/images/random")
        .then((response) => {
          this.RandomImageBreeds.push(response.data.message);
          this.allBreedWithRandomImage[breed] = response.data.message;
        })
        .catch((e) => {
          console.log(e);
        });
    });
  }

  public handleSizeChange(val: number) {
    this.pageSize = val;

    this.allBreedsFiltered = this.allBreeds.slice(
      this.pageNumber * this.pageSize - this.pageSize,
      this.pageNumber * this.pageSize
    );
    this.RandomImageBreedsFiltered = this.RandomImageBreeds.slice(
      this.pageNumber * this.pageSize - this.pageSize,
      this.pageNumber * this.pageSize
    );
  }

  public handleCurrentChange(val: number) {
    this.pageNumber = val;

    this.allBreedsFiltered = this.allBreeds.slice(
      this.pageNumber * this.pageSize - this.pageSize,
      this.pageNumber * this.pageSize
    );
    this.RandomImageBreedsFiltered = this.RandomImageBreeds.slice(
      this.pageNumber * this.pageSize - this.pageSize,
      this.pageNumber * this.pageSize
    );
  }

  mounted() {
    this.allBreedsFiltered = this.allBreeds;
    this.getAllBreeds();
  }
}
</script>


<style scoped lang="scss">
.el-image-component {
  width: 250px;
  height: 187px;
  overflow: inherit;
  -webkit-filter: blur(0px);
  filter: blur(0px);
}
.el-image-component:hover {
  -webkit-filter: blur(1px);
  filter: blur(1px);
}
.per-page-pagination {
  justify-content: right;

  display: flex;

  flex-wrap: wrap;

  max-width: 1360px;

  padding: 0px 0px 15px 0px;
  margin: 0 auto;
}
.page-pagination {
  justify-content: center;
  display: flex;
  flex-wrap: wrap;
  max-width: 960px;
  padding: 25px 90px 55px 50px;
  margin: 0 auto;
}
.image-grid {
  justify-content: center;
  display: flex;
  flex-wrap: wrap;
  max-width: 1360px;
  margin: 0 auto;
}
.grid-image {
  display: block;
  flex-basis: 100%;
  padding: 10px;
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

.viu-button--secondary:hover {
  background: #000;
  border-color: #000;
  color: #fff;
}
.viu-button {
  font-family: monaco, Consolas, Lucida Console, monospace;
  background: #fafafa;
  border: 0px solid #000;
  border-width: 0;
  color: #000;
  align-items: center;
  cursor: pointer;

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
.uppercase {
  font-size: 14px;
  line-height: 22px;
  text-transform: uppercase;
}
</style>
