<template>
  <div class="breed">
    <div class="main-div">
      <div class="per-page-pagination">
        <div v-on:click="routerPushBreedsGridPage()">
          <el-button
            class="home-page-button"
            type="plain"
            size="mini"
            icon="el-icon-arrow-left"
            >Previous Page</el-button
          >
        </div>
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          background
          :page-sizes="[5, 10, 15]"
          :page-size="this.pageSize"
          layout="total ,sizes"
          :total="this.randomImageBreed.length"
        >
        </el-pagination>
      </div>
      <div class="image-grid">
        <div
          class="grid-image"
          v-for="(breed, index) in randomImageBreedFiltered"
          :key="index"
        >
          <div class="container">
            <el-image
              class="centered project-image-bg el-image-component"
              :alt="breed"
              lazy
              :src="breed"
              :preview-src-list="[...breed]"
            >
            </el-image>

            <div class="overlay">
              <a href="#" class="icon" title="click to see image full size">
                <i class="fas fa-expand-arrows-alt"></i>
              </a>
            </div>
          </div>
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
        :total="this.randomImageBreed.length"
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
  @Prop() private breed!: string;

  private pageSize = 10;
  private pageNumber = 1;

  private randomImageBreed: string[] = [];
  private randomImageBreedFiltered: string[] = [];

  public async getAllRandomImageBreed() {
    const { data } = await axios.get(
      "https://dog.ceo/api/breed/" + this.breed + "/images"
    );
    this.randomImageBreed = data.message;

    this.handleCurrentChange(1);
  }

  public handleSizeChange(val: number) {
    this.pageSize = val;

    this.randomImageBreedFiltered = this.randomImageBreed.slice(
      this.pageNumber * this.pageSize - this.pageSize,
      this.pageNumber * this.pageSize
    );
  }

  public handleCurrentChange(val: number) {
    this.pageNumber = val;

    this.randomImageBreedFiltered = this.randomImageBreed.slice(
      this.pageNumber * this.pageSize - this.pageSize,
      this.pageNumber * this.pageSize
    );
  }

  public routerPushBreedsGridPage() {
    this.$router.push({
      name: "Home",
    });
  }

  mounted() {
    this.getAllRandomImageBreed();
  }
}
</script>


<style scoped lang="scss">
$white: #ffffff;
$black: #000;

.main-div {
  padding: 55px 0px 15px 0px;
}
.home-page-button {
  margin-left: 15px;
}
.el-image-component {
  width: 250px;
  height: 187px;
  overflow: inherit;
  -webkit-filter: blur(0px);
  filter: blur(0px);
  box-shadow: 4px -0px 8px 0 rgba(0, 0, 0, 0.2);
  -webkit-box-shadow: 4px -0px 8px 0 rgba(0, 0, 0, 0.2);
  -moz-box-shadow: 4px -0px 8px 0 rgba(0, 0, 0, 0.2);
  -ms-box-shadow: 4px -0px 8px 0 rgba(0, 0, 0, 0.2);
  -o-box-shadow: 4px -0px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  &:hover {
    -webkit-filter: blur(1px);
    filter: blur(1px);
  }
}
.per-page-pagination {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  max-width: 1360px;
  padding: 0px 0px 15px 0px;
  margin: 0 auto;
}
.top-icon {
  padding-left: 25px;
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
.container {
  position: relative;
  width: 100%;
  max-width: 400px;
  &:hover {
    .overlay {
      opacity: 1;
    }
  }
}
.image {
  width: 100%;
  height: auto;
}
.overlay {
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
  width: 100%;
  opacity: 0;
  transition: 0.3s ease;
  background-color: transparent;
  pointer-events: none;
}
.icon {
  color: $white;
  font-size: 100px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  text-align: center;
}
.fa-user {
  &:hover {
    color: #eee;
  }
}
@media only screen and (min-width: 640px) {
  .grid-image {
    flex-basis: 50%;
  }
}
@media only screen and (min-width: 960px) {
  .grid-image {
    flex-basis: 33.333%;
  }
}
@media only screen and (min-width: 1280px) {
  .grid-image {
    flex-basis: 25%;
  }
}
@media only screen and (min-width: 1600px) {
  .grid-image {
    flex-basis: 20%;
  }
}
</style>
