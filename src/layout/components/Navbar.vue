<template>
  <div class="navbar">
    <!-- 汉堡包组件 -->
    <hamburger
      :is-active="sidebar.opened"
      class="hamburger-container"
      @toggleClick="toggleSideBar"
    />

    <!-- title -->
    <div class="app-breadcrumb">
      黑马程序员
      <span class="breadBtn">体验版</span>
    </div>
    <div class="right-menu">
      <!-- 切换语言组件 -->
      <lang />
      <!-- 全屏组件 -->
      <full-screen />
      <el-dropdown class="avatar-container" trigger="click">
        <div class="avatar-wrapper">
          <!-- 用户头像 -->
          <img src="@/assets/common/bigUserHeader.png" class="user-avatar">
          <!-- 用户名称 -->
          <span class="name">赵阳老师</span>
          <i class="el-icon-caret-bottom" style="color:#fff" />
        </div>
        <!-- 下拉内容 -->
        <el-dropdown-menu slot="dropdown" class="user-dropdown">
          <router-link to="/">
            <el-dropdown-item> 首页 </el-dropdown-item>
          </router-link>
          <a target="_blank">
            <el-dropdown-item> 项目地址 </el-dropdown-item>
          </a>
          <el-dropdown-item divided @click.native="logout">
            <span style="display: block">退出登录</span>
          </el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Hamburger from '@/components/Hamburger'
import Lang from '@/components/Lang'
import FullScreen from '@/components/FullScreen'
export default {
  components: {
    Hamburger,
    Lang,
    FullScreen
  },
  computed: {
    ...mapGetters([
      'sidebar'
    ])
  },
  methods: {
    // 点击汉堡包
    toggleSideBar() {
      // 切换侧边栏的展开与收起
      this.$store.dispatch('app/toggleSideBar')
    },
    // 退出登录
    logout() {
      this.$router.push('/login')
    }
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  height: 50px;
  overflow: hidden;
  position: relative;
  background-image: -webkit-linear-gradient(left, #3d6df8, #5b8cff);
  box-shadow: 0 1px 4px rgba(0, 21, 41, 0.08);
  .app-breadcrumb {
    display: inline-block;
    font-size: 18px;
    line-height: 50px;
    margin-left: 10px;
    color: #ffffff;
    cursor: text;
    .breadBtn {
      background: #84a9fe;
      font-size: 14px;
      padding: 0 10px;
      display: inline-block;
      height: 30px;
      line-height: 30px;
      border-radius: 10px;
      margin-left: 15px;
    }
  }
  .user-avatar {
    cursor: pointer;
    width: 30px;
    height: 30px;
    border-radius: 15px;
    vertical-align: middle;
  }
  .name {
    color: #fff;
    vertical-align: middle;
    margin-left: 5px;
  }
  .user-dropdown {
    color: #fff;
  }

  .hamburger-container {
    line-height: 46px;
    height: 100%;
    float: left;
    cursor: pointer;
    transition: background 0.3s;
    -webkit-tap-highlight-color: transparent;

    &:hover {
      background: rgba(0, 0, 0, 0.025);
    }
  }

  .breadcrumb-container {
    float: left;
  }

  .right-menu {
    float: right;
    display:  flex;
    justify-content: center;
    align-items: center;

    &:focus {
      outline: none;
    }

    .right-menu-item {
      display: inline-block;
      padding: 0 8px;
      height: 100%;
      font-size: 18px;
      color: #5a5e66;
      vertical-align: text-bottom;

      &.hover-effect {
        cursor: pointer;
        transition: background 0.3s;

        &:hover {
          background: rgba(0, 0, 0, 0.025);
        }
      }
    }

    .avatar-container {
      margin-right: 30px;

      .avatar-wrapper {
        margin-top: 5px;
        position: relative;

        .user-avatar {
          cursor: pointer;
          width: 40px;
          height: 40px;
          border-radius: 10px;
        }

        .el-icon-caret-bottom {
          cursor: pointer;
          position: absolute;
          right: -20px;
          top: 14px;
          font-size: 12px;
        }
      }
    }
  }
}
</style>
