<template>
  <div style="height:auto;">
    <Sidebar 
      @search-input-emit="search"
    />
    <router-view></router-view>
  </div>
</template>

<script>
import Sidebar from "@/components/Sidebar.vue"

export default {
  name: "App",
  components: {
    Sidebar,
  },
  methods: {
    search(val) {
      
    }
  }
}
</script>

<style>
</style>