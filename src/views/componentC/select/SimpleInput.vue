<!-- 简单的 输入框组件 -->
<template>
  <div class="xSelect_container">
    <div style="width: 90px" class="xSelect_label">
      <span class="xSelect_check" v-show="isCheck"></span>
      <span class="label_title"
        >{{ defaultConfig.title
        }}<i v-show="isIcon" class="el-icon-warning-outline label_icon"></i
        ><span v-show="isIcon" class="douhao"> : </span></span
      >
      <span v-show="isIcon" class="icon_tip"
        >1%=100基点 <span class="sanjiao"></span
      ></span>
    </div>
    <div class="xSelect_wrap" style="width: calc(100% - 90px); height: '32px'">
      <el-input
        @blur="blurEvent"
        :type="inputType"
        v-model="value"
        placeholder="请输入"
        :disabled="isDisabled"
        v-debounce="{ handler: inputChange, event: 'input', wait: 5000 }" 
      ></el-input>
    </div>
    <div v-show="isShowTip" class="xSelect_tip">{{ defaultTip }}</div>
  </div>
</template>

<script>
export default {
  name: "SimpleInput",
  components: {},
  props: {
    isDisabled: {
      type: Boolean,
      default: false,
    },
    inputType: {
      type: String,
      default: "text",
    },
    defaultConfig: {
      type: Object,
      default: () => {},
    },
    isCheck: {
      type: Boolean,
      default: false,
    },
    isIcon: {
      type: Boolean,
      default: false,
    },
    // 当前使用组件 的 类型
    titleType: {
      type: String,
      default: "",
    },
    // 公共的清空 input的值
    commomClear: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      value: "",
      isShowTip: false, //是否显示tip
      defaultTip: "此项必填",
    };
  },
  watch: {
    commomClear(val) {
      if (val && this.titleType == "singleBApplyApplyNnumber") {
        // 单笔业务 申请编号
        this.value = "";
        this.$emit("changeSingleBApplyApplyNnumber", false);
      }
    },
  },
  created() {},
  methods: {
    blurEvent() {
      if (this.isCheck) {
        if (this.value.trim() == "") {
          this.isShowTip = true;
        } else {
          this.isShowTip = false;
        }
      }
    },
    inputChange() {
      this.$emit("inputValue", this.value);
    },
    handleSearch(value){
      console.log(value);
    }
  },
};
</script>
<style  lang="scss" scoped>
@import "./css/input.scss";
.douhao {
  margin-right: 3px;
  font-weight: bolder;
}
.xSelect_label {
  position: relative;
  .icon_tip {
    position: absolute;
    top: -15px;
    right: 4px;
    background: #000000;
    width: 85px;
    font-size: 12px;
    height: 16px;
    line-height: 16px;
    color: #fff;
    text-align: center;
    .sanjiao {
      position: absolute;
      top: -14px;
      right: -19px;
      display: inline-block;
      margin: 30px;
      width: 0px;
      height: 0px;
      border: 6px solid;
      border-color: #000 transparent transparent transparent;
    }
  }
}
</style>
