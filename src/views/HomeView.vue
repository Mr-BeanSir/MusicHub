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
    <div @click="cardLeft" class="arrow">
      <el-icon class="icon"><ArrowLeftBold /></el-icon>
    </div>
    <div class="main">
      <ul
        @mousedown="mD('random')"
        @mousemove="mouseMove('random')"
        @mouseup="mU('random')"
        @mouseleave="mU('random')"
        style="left: 0; transition: 0.4s"
        ref="card-main-random-ul"
        class="ul"
      >
        <li @click="test('random')" :key="item.name" v-for="item in songSheet">
          <el-card :body-style="{ padding: '0px' }" class="card-main">
            <img
                :src="item.img"
                style="width: 100%"
                draggable="false"
            />
            <p class="title">{{ item.name }}</p>
          </el-card>
        </li>
      </ul>
    </div>
    <div class="arrow">
      <el-icon @click="cardRight" class="icon"><ArrowRightBold /></el-icon>
    </div>
  </div>
</template>
<script>
import { Search, ArrowLeftBold, ArrowRightBold } from "@element-plus/icons-vue";

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
    Search,
    ArrowLeftBold,
    ArrowRightBold,
  },
  methods: {
    jumpSheet(id) {
      if (Math.abs(this.cardX - parseInt(this.$refs["card-main-" + id + "-ul"].style.left.replace("px", ""))) < 15) {

      }
    },
    searchCss(e) {
      if (e) {
        this.$refs["search-box"].style.border = "1px rgb(64,158,255) solid";
        this.$refs["search-box"].style.boxShadow = "0 0 5px rgb(64,158,255)";
      } else {
        this.$refs["search-box"].style.border = "1px rgb(229, 229, 229) solid";
        this.$refs["search-box"].style.boxShadow = "none";
      }
    },
    cardLeft() {
      let i = parseInt(this.$refs["card-main-random-ul"].style.left.replace("px", ""))
      if (i + 200 > 0) {
        this.$refs["card-main-random-ul"].style.left = "0";
      } else {
        this.$refs["card-main-random-ul"].style.left = i + 200 + "px";
      }
    },
    cardRight() {
      let i = parseInt(this.$refs["card-main-random-ul"].style.left.replace("px", ""))
      if (Math.abs(i - 200) > (this.songSheet.length - 4) * 200) {
        this.$refs["card-main-random-ul"].style.left = -(this.songSheet.length - 4) * 200 + "px";
      } else {
        this.$refs["card-main-random-ul"].style.left = i - 200 + "px";
      }
    },
    mD(id) {
      this.mouse = true;
      this.mouseClickX = window.event.screenX;
      this.cardX = parseInt(this.$refs["card-main-" + id + "-ul"].style.left.replace("px", ""));
      this.$refs["card-main-" + id + "-ul"].style.transition = "";
    },
    mU(id) {
      this.mouse = false;
      this.$refs["card-main-" + id + "-ul"].style.transition = "0.4s";
    },
    mouseMove(id) {
      if (this.mouse) {
        let i = this.cardX;
        let move = window.event.screenX - this.mouseClickX;
        if (move < 0) {
          if (Math.abs(i + move) > (this.songSheet.length - 4) * 200) {
            this.$refs["card-main-" + id + "-ul"].style.left = -(this.songSheet.length - 4) * 200 + "px";
          } else {
            this.$refs["card-main-" + id + "-ul"].style.left = i + move + "px";
          }
        } else {
          if (i + move > 0) {
            this.$refs["card-main-" + id + "-ul"].style.left = "0";
          } else {
            this.$refs["card-main-" + id + "-ul"].style.left = i + move + "px";
          }
        }
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
  .main {
    flex-grow: 1;
    margin: 0 20px 20px;
    display: flex;
    overflow: hidden;
    position: relative;
    border-radius: 5px;
    .ul {
      display: flex;
      position: relative;
    }
    .card-main {
      width: 200px;
      height: 200px;
      overflow: hidden;
      margin: 0 5px;
      flex-shrink: 0;
      position: relative;
      .title {
        width: 200px;
        bottom: 5px;
        left: 5px;
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
        color: white;
        position: absolute;
      }
      :hover {
        cursor: pointer;
      }
    }
  }
  .arrow {
    border: 1px grey solid;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    color: #565555;
    .icon {
      width: 40px;
      height: 40px;
      border-radius: 50%;
    }
    :hover {
      cursor: pointer;
    }
  }
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
