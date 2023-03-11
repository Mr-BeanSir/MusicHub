<template>
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
          <img :src="item.img" style="width: 100%" draggable="false" />
          <p class="title">{{ item.name }}</p>
        </el-card>
      </li>
    </ul>
  </div>
  <div class="arrow">
    <el-icon @click="cardRight" class="icon"><ArrowRightBold /></el-icon>
  </div>
</template>

<script>
import { ArrowLeftBold, ArrowRightBold } from "@element-plus/icons-vue";

export default {
  name: "HomeListComponents",
  props: ["songSheet"],
  components: {
    ArrowLeftBold,
    ArrowRightBold,
  },
  methods: {
    jumpSheet(id) {
      if (
        Math.abs(
          this.cardX -
            parseInt(
              this.$refs["card-main-" + id + "-ul"].style.left.replace("px", "")
            )
        ) < 15
      ) {
        console.log(123);
      }
    },
    cardLeft() {
      let i = parseInt(
        this.$refs["card-main-random-ul"].style.left.replace("px", "")
      );
      if (i + 200 > 0) {
        this.$refs["card-main-random-ul"].style.left = "0";
      } else {
        this.$refs["card-main-random-ul"].style.left = i + 200 + "px";
      }
    },
    cardRight() {
      let i = parseInt(
        this.$refs["card-main-random-ul"].style.left.replace("px", "")
      );
      if (Math.abs(i - 200) > (this.songSheet.length - 4) * 200) {
        this.$refs["card-main-random-ul"].style.left =
          -(this.songSheet.length - 4) * 200 + "px";
      } else {
        this.$refs["card-main-random-ul"].style.left = i - 200 + "px";
      }
    },
    mD(id) {
      this.mouse = true;
      this.mouseClickX = window.event.screenX;
      this.cardX = parseInt(
        this.$refs["card-main-" + id + "-ul"].style.left.replace("px", "")
      );
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
            this.$refs["card-main-" + id + "-ul"].style.left =
              -(this.songSheet.length - 4) * 200 + "px";
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
</style>
