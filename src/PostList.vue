<template>
  <view class="Container">
    <template v-if="isLoading">
      <view
        :style="{
          flex: 1,
          justifyContent: 'center'
        }">
        <activity-indicator size="large" color="#57C292" />
      </view>
    </template>
    <template
      v-if="!isLoading">
      <scroll-view class="ContainerPosts">
        <Card
          v-for="(post, index) in posts"
          :item="post"
          :navigation="navigation"
          :key="index" />
      </scroll-view>
    </template>
  </view>
</template>

<script>
import axios from 'axios'
import { parseString } from 'react-native-xml2js'
import Card from './Card'

const VUEJS_BRAZIL_URI = 'http://vuejs-brasil.com.br/feed.xml'
const parseXMLPromised = xml => new Promise((resolve, reject) => {
  parseString(xml, (err, json) => err ? reject(err) : resolve(json))
})

export default {
  name: 'PostList',
  props: {
    navigation: { type: Object, default: () => ({}) }
  },
  data: () => ({
    isLoading: false,
    posts: []
  }),
  components: { Card },
  async created () {
    try {
      this.isLoading = true;
      const { data: xml } = await axios.get(VUEJS_BRAZIL_URI)
      const json = await parseXMLPromised(xml)
      this.posts = json.rss.channel[0].item
      this.isLoading = false
    } catch (error) {
      console.log('* Error', error)
      this.isLoading = false
    }
  }
}
</script>

<style>
.Container {
  height: 100%;
  width: 100%;
}
.ContainerPosts {
  padding: 10px 5px;
}
</style>