<!-- 双input -->
<template>
  <div class="xSelect_container">
    <div :style="{ width: '92px' }" class="xSelect_label">
      {{ defaultConfig.title }}
    </div>
    <div class="xSelect_wrap" :style="{ width: 'calc(100% - 94px)' }">
      <el-input
        class="input"
        v-model="input1"
        @change="inputbefore"
        placeholder="请输入金额"
        type="number"
      ></el-input>
      <div class="interval">~</div>
      <el-input
        class="input input2"
        v-model="input2"
        @change="inputAfter"
        placeholder="请输入金额"
        type="number"
      ></el-input>
    </div>
  </div>
</template>

<script>
export default {
  name: "DoubleInput",
  components: {},
  props: {
    defaultConfig: {
      type: Object,
      default: () => {},
    },
    // 公共的清空 input的值
    commomClear: {
      type: Boolean,
      default: false,
    },
    titleType: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      input1: "",
      input2: "",
    };
  },
  watch: {
    commomClear(val) {
      if (val && this.titleType == "byLetterFAmount") {
        this.input1 = "";
        this.input2 = "";
        this.$emit("changeByLetterFAmount", false);
      }
    },
  },
  methods: {
    inputbefore() {
      this.$emit("acceptInputData1", this.input1);
    },
    inputAfter() {
      this.$emit("acceptInputData2", this.input2);
    },
  },
};
</script>
<style  lang="scss" scoped>
@import "./css/input.scss";
.xSelect_wrap {
	float: left;
  position: relative;
  line-height: 32px;
  height: 32px;
  overflow: hidden;
  border: 1px solid #dcdfe6;
  & > .input {
    border: none;
    outline: none;
    height: 30px;
    line-height: 30px;
    width: 45%;
  }
  & > .input {
    float: left;
  }
  & > .input2 {
    float: right;
  }
  & > .interval {
    z-index: 10;
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    margin: auto;
    width: 10px;
    height: 10px;
    line-height: 10px;
    color: #c0c4cc;
  }
}
::-webkit-input-placeholder {
  color: #c0c4cc;
}
::v-deep .el-input__inner {
  text-align: center;
  height: 30px;
  border: none;
  font-size: 12px;
  padding: 0;
  margin: 0;
}
</style>
