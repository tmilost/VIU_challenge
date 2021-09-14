<template>
  <div>
    <el-menu class="el-menu-demo" mode="horizontal">
      <div class="menuItems">
        <div class="menu-items">
          <el-menu-item v-on:click="toLink(config.shopviu)">
            <img
              class="menu-item-image"
              src="../assets/viuLogo.png"
              alt="VIU logo"
            />
          </el-menu-item>
          <el-menu-item
            v-on:click="toLink(config.linkedInUrl)"
            class="menu-item"
            ><i class="fab fa-linkedin"></i
          ></el-menu-item>
          <el-menu-item v-on:click="toLink(config.gitUrl)" class="menu-item"
            ><i class="fab fa-github"></i
          ></el-menu-item>
          <el-menu-item v-on:click="toLink(config.instagramUrl)" class="menu-item"
            ><i class="fab fa-instagram"></i
          ></el-menu-item>
          <el-menu-item v-on:click="toLink(config.cvUrl)" class="menu-item"
            ><i class="fas fa-address-card"></i
          ></el-menu-item>
        </div>
      </div>
    </el-menu>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { default as config } from "../assets/config.json";

@Component
export default class NavMenu extends Vue {
  public config = config;

  public toLink(adress: any) {
    window.location.href = adress;
  }
}
</script>


<style lang="scss" scoped>
.menu-items {
  justify-content: center;

  display: flex;
}
.el-menu-item {
  width: 575px;
}
.menu-item-image {
  float: left;
  width: 89px;
  height: 30px;
  padding-top: 12px;
}
.menu-item {
  float: right;
  width: 59px;
}
</style>