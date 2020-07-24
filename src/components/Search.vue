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

</style>
