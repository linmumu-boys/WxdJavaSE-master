<template>
  <div class="sidebar">
    <el-menu
        class="sidebar-el-menu"
        :default-active="onRoutes"
        :collapse="collapse"
        background-color="#324157"
        text-color="#bfcbd9"
        active-text-color="#20a0ff"
        unique-opened
        router
    >
      <template v-for="item in items">
          <el-menu-item :index="item.index" :key="item.index">
            <i :class="item.icon"></i>
            <span slot="title">{{ item.title }}</span>
          </el-menu-item>
      </template>
    </el-menu>
  </div>
</template>

<script>
import bus from '../common/bus';

export default {
  data() {
    return {
      collapse: false,
      items: [
        {
          icon: 'el-icon-pie-chart',
          index: 'BasicInformationTable',
          title: '设备基本信息表'
        },
        {
          icon: 'el-icon-pie-chart',
          index: 'GameInformationStatistics',
          title: '游戏信息统计表'
        },
        {
          icon: 'el-icon-pie-chart',
          index: 'ExceptionInformationTable',
          title: '异常信息表'
        },
        {
          icon: 'el-icon-pie-chart',
          index: 'Listofabnormalinformation',
          title: '异常信息明细表'
        },
        // {
        //   icon: 'el-icon-pie-chart',
        //   index: 'MaintenanceInformationSheet',
        //   title: '维修信息表'
        // }
      ]
    };
  },
  computed: {
    onRoutes() {
      return this.$route.path.replace('/', '');
    }
  },
  created() {
    // 通过 Event Bus 进行组件间通信，来折叠侧边栏
    bus.$on('collapse', msg => {
      this.collapse = msg;
      bus.$emit('collapse-content', msg);
    });
  }
};
</script>

<style scoped>
.sidebar {
  display: block;
  position: absolute;
  left: 0;
  top: 70px;
  bottom: 0;
  overflow-y: scroll;
}

.sidebar::-webkit-scrollbar {
  width: 0;
}

.sidebar-el-menu:not(.el-menu--collapse) {
  width: 250px;
}

.sidebar > ul {
  height: 100%;
}

</style>
