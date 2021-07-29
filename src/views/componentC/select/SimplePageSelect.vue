<!-- 一个简单的 带有分页的下拉菜单组件 -->
<template>
  <div class="xSelect_container">
    <div
      class="select_box"
      style="width: calc(100% - 94px)"
      ref="select_box"
      v-clickoutside="clickoutside"
    >
      <div class="select_wrap" @click="selectClick">
        <div
          class="current_value defaultC"
          v-if="selectionBoxDefaultValue == '请选择'"
        >
          {{ selectionBoxDefaultValue }}
        </div>
        <div class="current_value activeC" v-else>
          {{ selectionBoxDefaultValue }}
        </div>
        <div ref="triangle" class="triangle_container">
          <i class="el-icon-arrow-down"></i>
        </div>
      </div>

      <div
        class="option_wrapper"
        ref="optionwrapper"
        style="display: none; zindex: 1995"
      >
        <div style="max-height: 286px;">
          <ul ref="optionul">
            <li
              v-for="(item, idx) in subject"
              :key="idx"
              ref="optionitem"
              @click="itemClick(item)"
              @mouseover="move($event, idx)"
              @mouseout="out($event)"
              :class="item == currentName ? 'active' : ''"
            >
              <span class="li_right text_ellipsis">{{ item }}</span>
            </li>
          </ul>
        </div>
        <div>
          <el-pagination
            :current-page="paginationConfig.currentPage"
            :page-size="10"
            layout="total, prev, next"
            :total="paginationConfig.total"
            @prev-click="prevPageClick"
            @next-click="nextPageClick"
          >
          </el-pagination>
        </div>
      </div>
    </div>
    <span style="width: 94px" class="xSelect_label"
      ><span class="xSelect_check" v-show="isCheck"></span>
      <span class="label_title">
        {{ defaultLabelConfig.title }}
      </span>
    </span>
  </div>
</template>

<script>
import Clickoutside from "@/utils/clickoutside";
export default {
  name: "SimplePageSelect",
  components: {},
  directives: {
    //挂载指令
    Clickoutside,
  },
  props: {
    // 下拉菜单的数据
    subject: {
      type: Array,
      default() {
        return [];
      },
    },
    selectionBoxDefaultValue: {
      type: String,
      default: "请选择",
    },
    selectHeight: {
      default: 32,
    },
    currentName: {
      type: String,
      default: "",
    },
    paginationConfig: {
      type: Object,
      default: () => {},
    },
    isCheck: {
      type: Boolean,
      default() {
        return false;
      },
    },
    defaultLabelConfig: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      currentPage1: 1,
    };
  },
  computed: {
    optionWrapper() {
      //选项的节点
      return this.$refs.optionwrapper;
    },
    subjectList() {
      //选项的 item
      return this.$refs.optionitem;
    },
  },
  mounted() {
    this.$refs.select_box.style.height = this.selectHeight + "px";
    this.$refs.select_box.style.lineHeight = this.selectHeight + "px";
    this.$refs.optionwrapper.style.transition = 2 + "s";
  },
  methods: {
    isShow() {
      if (this.optionWrapper.style.display === "none") {
        this.optionWrapper.style.display = "block";
        this.$refs.triangle.classList.add("rotate_triangle_container");
      } else if (this.optionWrapper.style.display === "block") {
        this.optionWrapper.style.display = "none";
        this.$refs.triangle.classList.remove("rotate_triangle_container");
      }
    },

    // 点击了 头部的下拉菜单
    selectClick() {
      this.isShow();
      this.$emit("hideLoading");
      this.$refs.triangle.classList.add("rotate_triangle_container");
      let event = event || window.event
      this.optionWrapper.style.position = "fixed";
      this.optionWrapper.style.left = event.screenX-100 + 'px';
      this.optionWrapper.style.top = event.screenY-75 + 'px';
    },
    itemClick(item, idx) {
      this.isShow();
      this.$emit("changeSelect", item, idx);
    },
    move(event, idx) {
      for (let item of this.subjectList) {
        item.classList.remove("hover");
      }
      event.currentTarget.classList.add("hover");
    },
    out(event) {
      event.currentTarget.classList.remove("hover");
    },
    //点击外层的时候 触发的事件
    clickoutside() {
      if (this.optionWrapper.style.display === "block") {
        this.optionWrapper.style.display = "none";
        this.$refs.triangle.classList.remove("rotate_triangle_container");
      }
    },
    // 上一页
    prevPageClick(val) {
      this.$emit("nextPageClick", val);
    },
    // 下一页
    nextPageClick(val) {
      this.$emit("nextPageClick", val);
    },
  },
};
</script>
<style  lang="scss" scoped>
@import "./css/input.scss";
ul,
li {
  list-style: none;
}
.select_box {
  position: relative;
  font-size: 14px;
  float: right;
	/* overflow: hidden; */

  .select_wrap {
    width: 100%;
    height: 100%;
    border-radius: 4px;
    border: 1px solid #dcdfe6;
    background: #fff;
    z-index: 1994;
    position: relative;
    overflow: hidden;
  }

  .triangle_container {
    display: inline-block;
    position: absolute;
    top: 3%;
    right: 4%;
    i {
      color: #dcdfe6;
    }
  }
  .rotate_triangle_container {
    transform-origin: center 47%;
    transition: 0.2s;
    -webkit-transform: rotate(180deg);
    -moz-transform: rotate(180deg);
    -o-transform: rotate(180deg);
    -ms-transform: rotate(180deg);
    transform: rotate(180deg);
  }

  .active {
    color: #e82323;
    background: #f5f7fa !important;
    font-weight: 700;
  }
  .hover {
    color: #e82323;
    background: #f5f7fa !important;
  }
  .current_value {
    padding-left: 5px;
  }
  .defaultC {
    color: #c7c9cc;
    padding: 0 30px 0 17px;
  }
  .activeC {
    color: #606266;
    padding: 0 30px 0 17px;
  }
  .option_wrapper {
    position: absolute;
    z-index: 1995;
    left: 0px;
    top: 40px;
    width: 180px;
    padding-top: 10px;
    background: #f5f7fa;
    border: 1px solid #e4e7ed;
    border-radius: 4px;
    background-color: #fff;
    box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
    &::before {
      content: "";
      display: inline-block;
      width: 0;
      height: 0;
      border-left: 6px solid transparent;
      border-right: 6px solid transparent;
      border-bottom: 6px solid #fff;
      position: absolute;
      top: -6px;
      left: 14px;
    }
    ul {
      li {
        padding-left: 5px;
        height: 24px;
        line-height: 24px;
        margin-bottom: 2px;
        transition: 0.3s;
        background: #fff;
        cursor: pointer;
        .li_right {
          display: inline-block;
          width: 160px;
          padding-left: 6px;
        }
      }
    }
  }
}
::v-deep .el-pagination .btn-prev,
::v-deep .el-pagination .btn-next {
  background-color: transparent;
}
::v-deep .el-input__inner {
  height: 32px;
}
.el-pagination{
  padding: 0 5px ;
}
</style>
