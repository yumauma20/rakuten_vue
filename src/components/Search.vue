<template>
  <div>
    <div class="container">
      <input class="text" type="text" v-model="keyword" @keyup.enter="search">
      <input class="submit" type="submit" value="Search" @click="search">
    </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
  data() {
    return {
      keyword: "",
    }
  },
  methods: {
    async search() {
      this.$emit("loadStart")
      const { data } = await axios.get(`//app.rakuten.co.jp/services/api/IchibaItem/Search/20170706?applicationId=1071038582589670320&keyword=${ this.keyword }&sort=%2BitemPrice`);
      this.$emit("loadComplete", { results: data.results })
    }
  }
}

</script>

<style>
.container {
  display: flex;
  justify-content: center;
  height: 100px;
  padding: 20px;
  background-color: #355e3f;
  box-sizing: border-box;
}
 
 
.text {
  width: 50%;
  max-width: 300px;
  padding: 12px;
  border: none;
}
 
 
.submit {
  padding: .5em 2em;
  margin-left: 10px;
  color: #fff;
  background-color: #d33e10;
  border: none;
  border-radius: 20px;
}
</style>
