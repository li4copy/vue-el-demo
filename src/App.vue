<template>
  <div id="app">
    <el-drawer
      title="导航"
      custom-class="aside_msg"
      size="450px"
      :close-on-press-escape="true"
      :visible.sync="drawer"
    >
      <el-table
        :data="$fullRouter.options.routes"
        :show-header="false"
        row-class-name="row-pointer"
        style="width: 100%"
        @row-click="jump"
      >
        <el-table-column prop="path" label="链接" width="190">
        </el-table-column>
        <el-table-column prop="name" label="描述"> </el-table-column>
      </el-table>
      <!-- <div style="margin: 4px 0px;" v-for="router in $fullRouter.options.routes" :key="router.path">
         <router-link :to="router.path">{{router.name}}</router-link>
      </div> -->
    </el-drawer>
    <el-container class="ctner">
      <el-header class="header" height="">
        <i
          v-if="$route.path !== '/'"
          class="el-icon-arrow-left"
          @click="$router.go(-1)"
        ></i
        >{{ $route.name }}
        <!-- <svg><use xlink:href="#icon-test" /></svg> -->
        <!-- <el-badge class="item msg" @click.native="drawer = true">
          <i class="el-icon-menu"></i>
        </el-badge> -->
      </el-header>
      <el-main class="main">
        <transition name="test" mode="out-in">
          <router-view></router-view>
        </transition>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import MyImgViewer from "@/mixins/MyImgViewer/index";
export default {
  mixins: [MyImgViewer],
  data() {
    return {
      folded: true,
      drawer: false,
    };
  },
  methods: {
    jump(row) {
      this.$router.push(row.path);
      this.drawer = false;
    },
  },
};
</script>

<style>
.test-enter-active,
.test-leave-active {
  transition: all 0.2s;
}

.test-enter,
.test-leave-to {
  transform: translateX(-30px);
  opacity: 0;
}
</style>

<style lang="scss" scoped>
$h_height: 46px;
.header {
  background-color: #fff;
  position: fixed;
  height: #{$h_height};
  line-height: #{$h_height};
  box-shadow: 0px 3px 7px #cecece;
  width: 100%;
  z-index: 9;
}
.main {
  overflow: visible;
  height: 100vh;
  overflow-y: scroll;
  margin: #{$h_height} 0px 0px 0px;
  transition: margin-left 0.3s;
  -webkit-transition: margin-left 0.3s; /* Safari */
}

.msg {
  float: right;
  font-size: 23px;
  position: relative;
  top: 12px;
  right: 4px;
  cursor: pointer;
  line-height: 23px;
}

::v-deep .el-drawer.aside_msg {
  margin: 20px 20px 20px 0px;
  height: calc(100vh - 40px);
  border-radius: 9px;
}

::v-deep .el-drawer.aside_msg .el-drawer__header {
  margin-bottom: 8px;
}

::v-deep .el-drawer.aside_msg .el-drawer__body {
  padding: 0px 12px 0px 12px;
}

.title {
  float: left;
}
.time {
  float: right;
}
.readed div {
  color: rgb(156, 156, 156);
}
.title_wrapper {
  width: 100%;
}
.title_wrapper .el-badge {
  float: right;
}
.el-collapse ::v-deep .el-collapse-item__arrow {
  display: none;
}
::v-deep .row-pointer {
  cursor: pointer;
}
</style>
<style>
h3 {
  overflow-wrap: break-word;
}
img {
  width: 100%;
  display: block;
  margin: 0 auto;
}
</style>
