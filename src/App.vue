<template>
  <div id="app">
    <input type="text" v-model="search" @input="handleSearch" />
    <ul class="list">
      <li
        class="item"
        v-for="(item, idx) in searchList"
        :key="idx"
        @click="handleChoose(item.originalText)"
      >
        <span v-html="item.showText"></span>
      </li>
    </ul>
    <p>
      最终选择：<span>{{ finalChoose }}</span>
    </p>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      search: "",
      originList: [
        "1234",
        "123353",
        "24545",
        "15754",
        "111543",
        "33632",
        "16765",
      ],
      searchList: [],
      finalChoose: "",
    };
  },
  methods: {
    handleChoose(e) {
      console.log("e", e);
      this.finalChoose = e;
    },
    handleSearch(e) {
      this.searchList = [];
      const v = e.target.value;
      if (v) {
        this.originList.map((val) => {
          if (val.indexOf(v) !== -1) {
            this.searchList.push({
              showText: val.replaceAll(
                v,
                `<span style="color:red">${v}</span>`
              ),
              originalText: val,
            });
          }
        });
      } else {
        this.searchList = [];
      }
    },
  },
};
</script>

<style>
#app {
  margin: 0 auto;
  width: 300px;
  text-align: center;
  border: 1px solid #000;
}
.list {
  padding: 0;
  list-style: none;
}
.item {
  margin: 2px 0;
  border: 1px solid #00000010;
  cursor: pointer;
}
</style>
