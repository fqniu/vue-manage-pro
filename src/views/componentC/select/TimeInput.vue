<!-- 时间段 选择 -->
<template>
  <div class="xSelect_container">
    <div :style="{ width: '100px' }" class="xSelect_label">
      {{ defaultConfig.title }}
    </div>
    <div
      class="xSelect_wrap"
      :style="{ width: 'calc(100% - 100px)', height: '32px' }"
    >
      <el-date-picker
        v-model="value1"
        type="daterange"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
        value-format="yyyy-MM-dd"
        @change="selectData"
      >
      </el-date-picker>
    </div>
  </div>
</template>

<script>
export default {
  name: "TimeInput",
  components: {},
  props: {
    commomClear: {
      type: Boolean,
      default: false,
    },
    titleType: {
      type: String,
      default: "",
    },
    defaultConfig: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      value1: "",
    };
  },
  watch: {
    commomClear(val) {
      if (val && this.titleType == "byLetterClearFStart") {
        this.value1 = "";
        this.$emit("changeByLetterClearFStart", false);
      }
    },
  },
  methods: {
    selectData() {
      if (this.value1 == null) {
        this.$emit("acceptFinancingData", []);
      } else {
        this.$emit("acceptFinancingData", this.value1);
      }
    },
  },
};
</script>
<style  lang="scss" scoped>
@import "./css/input.scss";
::v-deep .el-date-editor {
  padding: 0 1px;
  width: 100%;
  border: none;
}
::v-deep .el-range-input {
  width: 40%;
  font-size: 12px;
}
::v-deep .el-range-separator {
  width: 8%;
  padding: 0;
  font-size: 12px;
  line-height: 34px;
}
::v-deep .el-range__icon {
  margin-top: -3px;
}
</style>
