/* eslint-disable vue/no-unused-components */
<template>
  <div class="navbar">
    <hamburger
      id="hamburger-container"
      :is-active="sidebar.opened"
      class="hamburger-container"
      @toggleClick="toggleSideBar"
    />

    <breadcrumb id="breadcrumb-container" class="breadcrumb-container" />

    <div class="right-menu">
      <template v-if="device !== 'mobile'">
        <!-- <search id="header-search" class="right-menu-item" /> -->

        <error-log class="errLog-container right-menu-item hover-effect" />

        <!-- <screenfull id="screenfull" class="right-menu-item hover-effect" /> -->
        <el-tooltip content="Global Size" effect="dark" placement="bottom">
          <!-- <size-select id="size-select" class="right-menu-item hover-effect" /> -->
          <!-- 下载图标 -->
          <el-button
            icon="el-icon-download"
            style="
              border: none;
              background: black;
              color: antiquewhite;
              position: absolute;
              right: 120px;
              margin-top: 10px;
            "
            class="download"
          />
        </el-tooltip>
        <!-- //图标按钮 -->
        <div class="messdiv">
          <el-tooltip
            content="管理系统"
            effect="dark"
            placement="bottom"
            style="color: antiquewhite"
          >
            <el-button>管理系统</el-button>
            <!-- <size-select id="size-select" class="right-menu-item hover-effect" /> -->
            <el-button
              icon="el-icon-s-operation"
              style="
                border: none;
                background: black;
                color: antiquewhite;
                position: absolute;
                right: 80px;
                margin-top: -10px;
              "
            />
          </el-tooltip>
          <div class="selecshow">
            <p>系统管理</p>
            <p>关于</p>
            <p>帮助管理</p>
          </div>
        </div>
      </template>

      <el-dropdown
        class="avatar-container right-menu-item hover-effect"
        trigger="click"
      >
        <div class="avatar-wrapper">
          <!-- <img :src="avatar + '?imageView2/1/w/80/h/80'" class="user-avatar"> -->
          <el-button
            icon="el-icon-user"
            style="border: none; background: black; color: antiquewhite"
          />
          <i
            class="el-icon-caret-bottom"
            style="position: absolute; right: 3px"
          />
        </div>
        <el-dropdown-menu slot="dropdown" style="width: 150px">
          <!-- <router-link to="/profile/index">
            <el-dropdown-item>Profile</el-dropdown-item>
          </router-link> -->
          <!-- <router-link to="/">
            <el-dropdown-item>Dashboard</el-dropdown-item>
          </router-link> -->
          <!-- 修改密码 -->
          <a target="_blank" href="">
            <el-dropdown-item
              style="
                margin-left: 14px;
                line-height: 50px;
                font-size: 16px;
                color: black;
              "
            >修改密码</el-dropdown-item>
          </a>
          <a
            target="_blank"
            href="https://panjiachen.github.io/vue-element-admin-site/#/"
          >
            <!-- 记忆标签 -->
            <!-- <el-dropdown-item>Docs</el-dropdown-item> -->
            <span style="margin-left: 25px">记忆标签</span>
            <el-switch
              v-model="value"
              active-color="#13ce66"
              inactive-color="#ff4949"
            />
          </a>
          <el-dropdown-item divided @click.native="logout">
            <span
              style="
                display: block;
                margin-left: 30px;
                font-size: 16px;
                color: black;
              "
            >退出</span>
          </el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Breadcrumb from '@/components/Breadcrumb'
import Hamburger from '@/components/Hamburger'
import ErrorLog from '@/components/ErrorLog'
import Sheenful from '@/components/Screenfull'
import SizeSelect from '@/components/SizeSelect'
import Search from '@/components/HeaderSearch'

export default {
  components: {
    Breadcrumb,
    Hamburger,
    ErrorLog,
    // eslint-disable-next-line vue/no-unused-components
    Screenfull: Sheenful,
    // eslint-disable-next-line vue/no-unused-components
    SizeSelect,
    // eslint-disable-next-line vue/no-unused-components
    Search
  },
  data() {
    return {
      value: true
    }
  },
  computed: {
    ...mapGetters(['sidebar', 'avatar', 'device'])
  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch('app/toggleSideBar')
    },
    async logout() {
      await this.$store.dispatch('user/logout')
      this.$router.push(`/login?redirect=${this.$route.fullPath}`)
    }
  }
}
</script>

<style lang="scss" scoped>
.navbar {
  height: 50px;
  overflow: hidden;
  position: relative;
  background: rgb(20, 20, 20);
  box-shadow: 0 1px 4px rgba(0, 21, 41, 0.08);

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
  .messdiv {
    position: relative;
    width: 150px;
    height: auto;
    font-size: 14px;
    margin: 20px 0 0 20px;
  }
  .selecshow {
    display: none;
    position: absolute;
    border: 1px solid #ccc;
    box-shadow: 0px 8px 16px 0px #666;
    padding: 10px;
    min-width: 140px;
    line-height: 30px;
  }
  .breadcrumb-container {
    float: left;
  }

  .errLog-container {
    display: inline-block;
    vertical-align: top;
  }

  .right-menu {
    float: right;
    height: 100%;
    line-height: 50px;

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
    .right-menu:hover .download {
      display: block;
    }
    .avatar-container {
      margin-right: 30px;

      .avatar-wrapper {
        position: relative;
        margin-top: -18px;
        margin-left: 60px;

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
          top: 25px;
          font-size: 12px;
        }
      }
    }
  }
}
</style>
