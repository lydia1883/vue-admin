<template>
  <div class="app-wrapper" :class="classObj">
    
    <div class="main-container">
      <navbar></navbar>
      <el-row type="flex" class="main-box">
        <el-col class="height100 sidebar-box">
          <sidebar class="sidebar-container"></sidebar>
        </el-col>
        <el-col  class="height100 appMainBox">
            <!-- <tags-view></tags-view> -->
            <app-main></app-main>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import { Navbar, Sidebar, AppMain, TagsView } from './components'
import ResizeMixin from './mixin/ResizeHandler'

export default {
  name: 'layout',
  components: {
    Navbar,
    Sidebar,
    AppMain,
    TagsView
  },
  mixins: [ResizeMixin],
  computed: {
    sidebar() {
      return this.$store.state.app.sidebar
    },
    device() {
      return this.$store.state.app.device
    },
    classObj() {
      return {
        hideSidebar: !this.sidebar.opened,
        withoutAnimation: this.sidebar.withoutAnimation,
        mobile: this.device === 'mobile'
      }
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
  @import "src/styles/mixin.scss";
  .app-wrapper {
    @include clearfix;
    position: relative;
    height: 100%;
    width: 100%;
  }

  .main-box {
    margin-top:100px;
    height: calc(100% - 100px)
  }

  .sidebar-box {
    flex: 0 0 180px;
  }
</style>
