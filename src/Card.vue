<template>
  <touchable-opacity
    class="Card"
    title="Button"
    :on-press="() => navigation.push('PostDetail', { content: item.description[0] })">
    <text class="CardTitle">{{ item.title[0] | wrap}}</text>
      <text class="CardDate">
        By <text class="BoldWord">Vue.js Brazil</text> on 
        <text class="BoldWord">{{ item.pubDate[0] | formatDate }}</text>
      </text>
  </touchable-opacity>
</template>

<script>
import { format } from 'date-fns'

export default {
  name: 'Card',
  props: {
    item: { type: Object, default: () => ({}) },
    navigation: { type: Object, default: () => ({}) }
  },
  filters: {
    wrap (value) {
      return value.slice(0, 30) + '...'
    },
    formatDate (value, pattern = 'DD/MM/YYYY') {
      return format(value, pattern)
    } 
  }
}
</script>

<style>
.Card {
  margin-bottom: 10px;
  height: 50px;
}
.CardTitle {
  color: #57C292;
  font-size: 20px;
  font-weight: bold;
}

.CardDate {
  color: #ccc;
  font-style: italic;
}

.BoldWord {
  font-weight: bold;
}
</style>
