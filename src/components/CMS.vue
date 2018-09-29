<template>
  <div style="background-color: #545c64; width: 100%; height: 100%; position: fixed;">
    <div style="background-color: gray; height: 100px;">Header</div>
    <div style=" float: left;">
      <el-menu
        style="width: 200px;"
        @open="handleOpen"
        @close="handleClose"
        background-color="#545c64"
        text-color="#fff"
        active-text-color="#ffd04b">
        <el-submenu index="1">
          <template slot="title">
            <i class="el-icon-location"></i>
            <span>导航一</span>
          </template>
          <el-menu-item-group>
            <template slot="title">分组一</template>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
          </el-menu-item-group>
          <el-menu-item-group title="分组2">
            <el-menu-item index="1-3">选项3</el-menu-item>
          </el-menu-item-group>
          <el-submenu index="1-4">
            <template slot="title">选项4</template>
            <el-menu-item index="1-4-1">选项1</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-menu-item index="2">
          <i class="el-icon-menu"></i>
          <span slot="title">导航二</span>
        </el-menu-item>
        <el-menu-item index="3" disabled>
          <i class="el-icon-document"></i>
          <span slot="title">导航三</span>
        </el-menu-item>
        <el-menu-item index="4">
          <i class="el-icon-setting"></i>
          <span slot="title">导航四</span>
        </el-menu-item>
      </el-menu>
    </div>
    <div style="float: left; background-color: orange;">
      <div style="width: 200px; height: 1000px;">
        1
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from '../components/HelloWorld'
export default {
  name: 'CMS',
  data () {
    return {
      isCollapse: true,
      editableTabsValue: 'n1',
      editableTabs: [{
        title: 'n1',
        name: 'n1',
        content: 'New Tab content n1'
      }]
    }
  },
  methods: {
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    },
    removeTab (targetName) {
      let tabs = this.editableTabs
      let activeName = this.editableTabsValue
      if (activeName === targetName) {
        tabs.forEach((tab, index) => {
          if (tab.name === targetName) {
            let nextTab = tabs[index + 1] || tabs[index - 1]
            if (nextTab) {
              activeName = nextTab.name
            }
          }
        })
      }
      this.editableTabsValue = activeName
      this.editableTabs = tabs.filter(tab => tab.name !== targetName)
    },
    addTab (targetName) {
      let newTabName = targetName + ''
      for (let i = 0; i < this.editableTabs.length; i++) {
        if (this.editableTabs[i].hasOwnProperty('title') && this.editableTabs[i].title === targetName) {
          this.editableTabsValue = newTabName
          console.log(newTabName)
          return
        }
      }
      this.editableTabs.push({
        title: targetName,
        name: newTabName,
        content: 'New Tab content' + targetName
      })
      this.editableTabsValue = newTabName
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
