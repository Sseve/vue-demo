<template>
  <el-menu default-active="1-4-1" class="el-menu-vertical-demo" background-color="#545c64" 
  text-color="#fff" active-text-color="#ffd04b" @open="handleOpen" @close="handleClose" 
  :collapse="isCollapse">
  <h3> {{isCollapse? '中台': '中台系统'}}</h3>
  <el-menu-item @click="clickMenu(item)" v-for="item in noChildren" :index="item.path" :key="item.path">
    <i :class="'el-icon-' + item.icon"></i>
    <span slot="title">{{item.label}}</span>
  </el-menu-item>
  <el-submenu v-for="item in hasChildren" :index="item.path" :key="item.path">
    <template slot="title">
      <i :class="'el-icon-' + item.icon"></i>
      <span slot="title">{{item.label}}</span>
    </template>
    <el-menu-item-group v-for="subItem in item.children" :key="subItem.path">
      <el-menu-item :index="subItem.path">{{subItem.label}}</el-menu-item>
    </el-menu-item-group>
  </el-submenu>
</el-menu>
</template>

<script>
  export default {
    data() {
      return {
        // 接口获取数据在侧边栏渲染
        menu: [
          {
            path: '/',
            name: '/main',
            label: '首页',
            icon: 's-home',
            url: 'main/index'
          },
          {
            label: '系统管理',
            icon: 'menu',
            path: '/system',
            children: [
              {
                path: '/page1',
                name: 'page1',
                label: '页面1',
                icon: 'setting',
                url: 'page1/index'
              },
              {
                path: '/page2',
                name: 'page2',
                label: '页面2',
                icon: 'setting',
                url: 'page2/index'
              }
            ]
          }
        ]
      };
    },
    methods: {
      handleOpen(key, keyPath) {
        console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
      clickMenu(item) {
        this.$router.push({
          name: item.name
        })
      }
    },
    computed: {
      noChildren() {
        return this.menu.filter(item => !item.children)
      },
      hasChildren() {
          return this.menu.filter(item => item.children)
      },
      isCollapse() {
        return this.$store.state.table.isCollapse
      }
    }
  }
</script>

<style lang="less" scoped>
  .el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
    min-height: 400px;
  }
  .el-menu {
    height: 100%;
    border: none;
    h3 {
      color: #fff;
      text-align: center;
      line-height: 48px;
    }
  }
</style>