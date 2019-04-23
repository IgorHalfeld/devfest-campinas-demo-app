<template>
  <scroll-view
    :style="{
      flex: 1,
      backgroundColor: '#fff',
    }">
    <HTMLContainer
      :html="getHTML()"
      :containerStyle="{ padding: 10 }" />
  </scroll-view>
</template>

<script>
import HTMLContainer from 'react-native-render-html'

export default {
  name: 'PostDetail',
  props: {
    navigation: { type: Object, default: () => ({}) }
  },
  components: {
    HTMLContainer
  },
  methods: {
    getHTML () {
      return this.navigation.getParam('content', '<h1>Nothing...</h1>')
    }
  }
}
</script>
