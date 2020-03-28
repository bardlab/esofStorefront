<template>
<div class="container max-w-5xl my-5">
      <h1 class="text-center text-5xl font-sans p-5 font-thin">ESOF Storefront</h1>
      <ul class="flex flex-row justify-between border-t border-gray-300 font-light text-lg">
            <li v-bind:class="isPageActive('/')"><a href="/">Home</a></li>
            <li v-bind:class="isPageActive('/browser')"><a href="/browser">Program Browser</a></li>
            <li v-bind:class="isPageActive('/about')"><a href="/about">About</a></li>
      </ul>
<!--      
      <button class="bg-blue-100 hover:bg-blue-200 rounded px-5">Browser</button>
      <button class="bg-blue-100 rounded px-5 rounded">About</button>
-->
</div>
</template>

<script>
export default {
      methods:{
            isPageActive(cur){
                  return {
                        "border-t-2 border-blue-300": this.$route.fullPath == cur
                  }
            }
      }
}
</script>