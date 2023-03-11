<template>
  <div class="search">
    <div
      class="search-box"
      ref="search-box"
      @mouseover="searchCss(true)"
      @mouseleave="searchCss(false)"
    >
      <input type="text" placeholder="请输入歌曲" class="search-input" />
      <el-icon class="search-icon">
        <Search />
      </el-icon>
    </div>
  </div>
  <p class="card-title">随机歌单</p>
  <div class="card">
    <HomeListComponents :song-sheet="songSheet" />
  </div>
</template>
<script>
import { Search } from "@element-plus/icons-vue";
import HomeListComponents from "@/components/HomeListComponents.vue";

export default {
  name: "HomeView",
  data() {
    return {
      songSheet: [
        {
          name: "古风伤恋｜待到红颜消 杳杳无归期",
          img: "http://p4.music.126.net/6QbE9r2JeqBz3j3Kva--4A==/109951163038217098.jpg?param=200y200",
          href: "https://music.163.com/#/playlist?id=948471242",
        },
        {
          name: "「欧美Live」惊艳现场版，嗨到停不下来!",
          img: "http://p4.music.126.net/ZtQOTgvhqrcWYapiPj9NWQ==/19018252626210242.jpg?param=200y200",
          href: "https://music.163.com/#/playlist?id=948471242",
        },
        {
          name: "夜晚温柔粤语女声 唱出谁的不眠心事",
          img: "http://p3.music.126.net/4uiy7t752A4HHF2bwqVj1A==/109951164812388197.jpg?param=200y200",
          href: "https://music.163.com/#/playlist?id=948471242",
        },
        {
          name: "夜晚温柔粤语女声 唱出谁的不眠心事",
          img: "http://p3.music.126.net/4uiy7t752A4HHF2bwqVj1A==/109951164812388197.jpg?param=200y200",
          href: "https://music.163.com/#/playlist?id=948471242",
        },
        {
          name: "夜晚温柔粤语女声 唱出谁的不眠心事",
          img: "http://p3.music.126.net/4uiy7t752A4HHF2bwqVj1A==/109951164812388197.jpg?param=200y200",
          href: "https://music.163.com/#/playlist?id=948471242",
        },
        {
          name: "夜晚温柔粤语女声 唱出谁的不眠心事",
          img: "http://p3.music.126.net/4uiy7t752A4HHF2bwqVj1A==/109951164812388197.jpg?param=200y200",
          href: "https://music.163.com/#/playlist?id=948471242",
        },
      ],
      mouse: false,
      mouseClickX: 0,
      cardX: 0,
    };
  },
  components: {
    HomeListComponents,
    Search,
  },
  methods: {
    searchCss(e) {
      if (e) {
        this.$refs["search-box"].style.border = "1px rgb(64,158,255) solid";
        this.$refs["search-box"].style.boxShadow = "0 0 5px rgb(64,158,255)";
      } else {
        this.$refs["search-box"].style.border = "1px rgb(229, 229, 229) solid";
        this.$refs["search-box"].style.boxShadow = "none";
      }
    },
  },
};
</script>

<style lang="less" scoped>
:root {
  --search-background: white;
}
.card-title {
  font-size: 26px;
}
.card {
  width: 100%;
  height: 300px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-around;
}
.search {
  display: flex;
  justify-content: center;
  margin: 60px 0 120px;
  .search-box {
    background-color: var(--search-background);
    width: 600px;
    border-radius: 40px;
    border: 1px rgb(229, 229, 229) solid;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    .search-input {
      padding: 0 45px 0 15px;
      border: none;
      outline: none;
      font-size: 16px;
      flex-grow: 1;
      height: 40px;
      background-color: var(--search-background);
    }
    .search-icon {
      font-size: 26px;
      color: grey;
      position: absolute;
      right: 10px;
      :hover {
        cursor: pointer;
      }
    }
  }
}
</style>
