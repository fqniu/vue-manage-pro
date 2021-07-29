<template>
  <div>
    <XSelect
      :subject="depositSubject"
      @changeSelect="changeSelect"
      :defaultValue="defaultValue"
      selectWidth="90"
      selectHeight="24"
      @hideLoading="hideLoading"
      :currentNum="currentNum"
      userType="depositSelect"
    ></XSelect>
    <div>
      {{ defaultValue }}
    </div>
    <div class="search_wrap">
      <div class="odd_number">
        <SimpleInput
          :defaultConfig="ApplyNnumber"
          titleType="singleBApplyApplyNnumber"
          :commomClear="singleBApplyApplyNnumber"
          @inputValue="ApplyNnumberChange"
          @changeSingleBApplyApplyNnumber="changeSingleBApplyApplyNnumber"
        />
      </div>
      <div class="odd_number">
        <DoubleInput
          :defaultConfig="FinancingAmount"
          @acceptInputData1="FinancingAmountChange1"
          @acceptInputData2="FinancingAmountChange2"
          :commomClear="byLetterFAmount"
          titleType="byLetterFAmount"
          @changeByLetterFAmount="changeByLetterFAmount"
        />
      </div>
      <div class="odd_number">
        <TimeInput
          :defaultConfig="FinancingStart"
          @acceptFinancingData="acceptFinancingStartData"
          :commomClear="byLetterClearFStart"
          titleType="byLetterClearFStart"
          @changeByLetterClearFStart="changeByLetterClearFStart"
        />
      </div>
      <div class="odd_number">
        <SimplePageSelect
          :defaultLabelConfig="dataDeadline"
          :isCheck="true"
          :subject="dataDeadlineSubject"
          :selectionBoxDefaultValue="dataDeadlineDefaultVal"
          :currentName="dataDeadlineCurrentName"
          :paginationConfig="dataDeadlinePage"
          @changeSelect="dataDeadlineChange"
          @nextPageClick="dataDeadlineNextPage"
        />
      </div>
    </div>
    <div class="resetBtn">
      <el-button @click="reast">重置</el-button>
    </div>
  </div>
</template>

<script>
import XSelect from "./Select";
import SimpleInput from "./SimpleInput.vue";
import DoubleInput from "./DoubleInput.vue";
import TimeInput from "./TimeInput.vue";
import SimplePageSelect from "./SimplePageSelect.vue";
export default {
  name: "SelectPage",
  components: {
    XSelect,
    SimpleInput,
    DoubleInput,
    TimeInput,
    SimplePageSelect,
  },
  data() {
    return {
      // 下拉菜单
      depositSubject: [
        {
          lab: "人民币",
          value: "CNY",
        },
        {
          lab: "美元",
          value: "USD",
        },
        {
          lab: "港币",
          value: "HKD",
        },
      ],
      defaultValue: "人民币",
      currentNum: 0, //默认选中
      currentValue: "CNY",
      ApplyNnumber: { title: "申请编号：" },
      singleBApplyApplyNnumber: false,
      FinancingAmount: {
        title: "融资金额：",
      },
      byLetterFAmount: false,
      FinancingStart: {
        title: "融资起始日：",
        placeholder: "请选择",
      },
      byLetterClearFStart: false,
      dataDeadline: { title: "数据截止日：" },
      dataDeadlineSubject: [],
      dataDeadlineDefaultVal: "请选择",
      dataDeadlineCurrentName: "",
      dataDeadlinePage: {
        currentPage: 1,
        total: 0,
      },
    };
  },
  created() {
    this.getDataDeal(1, 10);
  },
  methods: {
    // 下拉菜单
    changeSelect(item, idx) {
      this.defaultValue = item.lab; //后
      this.currentNum = idx;
      this.currentValue = item.value;
    },
    //隐藏 loader
    hideLoading() {
      console.log("点击 需要隐藏什么");
    },
    // 申请编号
    ApplyNnumberChange(val) {
      console.log("输入的值", val);
    },
    changeSingleBApplyApplyNnumber(flag) {
      this.singleBApplyApplyNnumber = flag;
    },
    // 融资金额
    FinancingAmountChange1(val) {
      console.log("融资金额1", val);
    },
    FinancingAmountChange2(val) {
      console.log("融资金额2", val);
    },
    changeByLetterFAmount(flag) {
      this.byLetterFAmount = flag;
    },
    // 融资起始日
    acceptFinancingStartData(arr) {
      console.log("融资起始日", arr);
    },
    changeByLetterClearFStart(flag) {
      this.byLetterClearFStart = flag;
    },
    // 获取数据截止日 请求拿到数据
    getDataDeal(val) {
      if (val == 1) {
        this.dataDeadlineSubject = [
          "111",
          "222",
          "333",
          "444",
          "555",
          "666",
          "777",
          "888",
          "999",
          "1010",
        ];
      } else {
        this.dataDeadlineSubject = ["1111", "2222"];
      }

      this.dataDeadlinePage.total = 12;
    },
    // 数据截止日：
    dataDeadlineChange(val) {
      this.dataDeadlineDefaultVal = val;
      this.dataDeadlineCurrentName = val;
      this.dataDeadlineVal = val;
    },
    dataDeadlineNextPage(val) {
      this.dataDeadlinePage.currentPage = val;
      this.getDataDeal(val, 10);
    },
    // 重置
    reast() {
      this.singleBApplyApplyNnumber = true;
      this.byLetterFAmount = true;
      this.byLetterClearFStart = true;
    },
  },
};
</script>
<style  lang="scss" scoped>
.search_wrap {
  width: 100%;
  clear: both;
}
.odd_number {
  width: 24%;
  margin-right: 1%;
  height: 32px;
  float: left;
  margin-bottom: 0.65rem;
  & > :nth-child(4n) {
    margin-right: 0;
  }
}
.resetBtn {
  clear: both;
}
</style>
