<template>
<!-- 首页的NavBar -->
  <div class="navbar">
    <hamburger id="hamburger-container" :is-active="sidebar.opened" class="hamburger-container" @toggleClick="toggleSideBar" />

    <weather v-if="device != 'mobile'" style="margin: 15px;float: left"/>


    <!-- <span>是否登录</span> -->
            <!-- 登录注册用户信息 -->
            <div class="right-menu-no-login">
              <el-button-group :style="{'margin-left': '20px'}">
                    <el-button round type="primary" plain @click="loginAndRegister(1)">登录</el-button>
                    <el-button round type="primary" plain @click="loginAndRegister(0)">注册</el-button>
                </el-button-group>

            </div>
    

  </div>
</template>

<script>
  import {mapGetters, mapState} from 'vuex'
  import { getToken } from '@/utils/auth'
  import ResizeMixin from '../mixin/ResizeHandler'

  import Hamburger from '@/components/Hamburger'
  import Weather from "@/components/Weather";


export default {
  components: {
    Weather,
    Hamburger
  },
  computed: {
    ...mapGetters([
      'sidebar',
      'avatar',
    ]),
    ...mapState({
      device: state => state.app.device,
    }),
  },
  mixins: [ResizeMixin],
  methods: {
    toggleSideBar() {
      this.$store.dispatch('app/toggleSideBar')
    },

  }
}
</script>

<style lang="scss" scoped>
.navbar {
  height: 50px;
  overflow: hidden;
  position: relative;
  background: #fff;
  box-shadow: 0 1px 4px rgba(0,21,41,.08);

  .hamburger-container {
    line-height: 46px;
    height: 100%;
    float: left;
    cursor: pointer;
    transition: background .3s;
    -webkit-tap-highlight-color:transparent;

    &:hover {
      background: rgba(0, 0, 0, .025)
    }
  }

  .right-menu-no-login{
    margin-right: 10px;
    height: 100%;
    float: right;
    line-height: 50px;
  }

  .errLog-container {
    display: inline-block;
    vertical-align: top;
  }

  .weather {
    float: left;
    margin-top: 15px;
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
        transition: background .3s;

        &:hover {
          background: rgba(0, 0, 0, .025)
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
          border-radius: 50%;
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
