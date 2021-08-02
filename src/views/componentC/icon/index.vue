<template>
  <div class="icon-style">
    <!-- 用法如下 -->
    <div v-for="(item, idx) in iconsList" :key="idx" class="icon-list">
      <item :icon="item.icon" :title="item.title" />
    </div>
  </div>
</template>

<script>
import Item from "@/components/SvgIcon/Item";
export default {
  name: "index",
  components: {
    Item,
  },
  data() {
    return {
      iconsList: [
        { icon: "user", title: "user" },
        { icon: "account", title: "account" },
        { icon: "authorization", title: "authorization" },
        { icon: "business", title: "business" },
        { icon: "dashboard", title: "dashboard" },
        { icon: "data", title: "data" },
        { icon: "edit", title: "edit" },
        { icon: "example", title: "example" },
        { icon: "exit", title: "exit" },
        { icon: "eye-open", title: "eye" },
        { icon: "eye", title: "eye" },
        { icon: "form", title: "form" },
        { icon: "list", title: "list" },
        { icon: "link", title: "link" },
        { icon: "nested", title: "nested" },
        { icon: "password", title: "password" },
        { icon: "product", title: "product" },
        { icon: "sms", title: "sms" },
        { icon: "table", title: "table" },
        { icon: "template", title: "template" },
        { icon: "tree", title: "tree" },
        { icon: "sms", title: "sms" },
      ],
    };
  },
  mounted() {},
  computed: {},
  methods: {},
};
</script>

<style  lang="scss">
.icon-style {
  background: #ccc;
  font-size: 14px;
  color: #000;
  display: flex;
  flex-wrap: wrap;
  flex-shrink: 0;
}
.svg-icon {
  margin-right: 20px;
}
.icon-list {
  width: 150px;
  height: 20px;
  background: #eee;
  margin: 20px;
  padding: 0 10px;
}
</style>

