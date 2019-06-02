<template>
  <div id="app">
    <div class="markdown-body">
      <my-markdown></my-markdown>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
    'my-markdown': () => import('./something-cool.md')
  }
}
</script>

<style lang="scss">
@import '~@/style/main.scss';

</style>
