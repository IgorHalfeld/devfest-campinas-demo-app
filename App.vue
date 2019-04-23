<template>
  <view class="Container">
    <view class="ContainerHeader">
      <text class="ContainerHeaderTitle">Vue.js Brazil Blog App!</text>
    </view>
    <app-navigation></app-navigation>
  </view>
</template>

<script>
import { StackNavigator } from "vue-native-router"
import PostList from './src/PostList'
import PostDetail from './src/PostDetail'

const routes = { PostList, PostDetail }
const AppNavigation = StackNavigator(routes, {
  initialRouteName: 'PostList',
  headerMode: 'none',
  backgroundColor: 'white',
})

export default {
  components: { AppNavigation }
}
</script>

<style>
.Container {
  height: 100%;
  width: 100%;
}
.ContainerHeader {
  background-color: #57C292;
  padding-top: 40px;
  height: 120px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.ContainerHeaderTitle {
  color: #fff;
  font-size: 20px;
  font-weight: bold;
}
</style>