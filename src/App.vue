<template>
  <div id="app">
    <div class="top_header">
      <Header />
    </div>
    <main>
      <Body id="Body"/>
    </main>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Body from '@/components/Body.vue'

export default {
  name: 'App',
  components: {
    Header,
    Body,
  }
}
</script>

<style lang="scss">
@import '@/styles/globals.scss';
</style>
