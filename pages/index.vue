<template>
  <div>
    <!--整屏滚动插件-->
    <div class='p-relative head-bg'>
      <div class='h-content'>
        <div class='h-conte'>
          <div class='_left'>

            <div class='Business'>{{ $t('index.oneTitle') }}</div>
            <div class='Services'>{{ $t('index.oneNameTwo') }}</div>
<!--            <div class='login-input' >-->
<!--              <el-input v-model='context' :placeholder="$t('header.placeholder')" class='c-input' style='color: #FFFFFF' />-->
<!--              &lt;!&ndash;          el-icon-search&ndash;&gt;-->
<!--              <i class="el-icon-search " @click='handleClick(3)' style='font-size: 24px'></i>-->
<!--              &lt;!&ndash;          <img style='width: 32px; height: 32px' src='~/assets/images/cloudSales/icon_sousuo.png' alt='' @click='handleClick(2)'/>&ndash;&gt;-->
<!--            </div>-->
            <div class='Potential'>{{ $t('index.oneContent') }}</div>
            <div class='Services'>{{ $t('index.oneName') }}</div>
            <div class='button-view' style='display: flex; width: 100%'>
<!--              <v-btn @click='handleClick(1)' height='50px' class='try-out-bt'-->
<!--                     style='margin-right: 20px;margin-bottom: 20px'>-->
                <img  src="../assets/images/ios.svg" @click='handleClick(1)'  style='margin-right: 20px;cursor: pointer'
                      alt=""/>
<!--                {{ $t('index.oneButtonLeft') }}-->
<!--              </v-btn>-->
<!--              <v-btn @click='handleClick(2)' height='50px' class='try-out-bt' style='margin-bottom: 20px;'>-->

                <img  src="../assets/images/playIcon.svg" @click='handleClick(2)'   style='margin-right: 20px;cursor: pointer'
                      alt=""/>
<!--                {{ $t('index.oneButtonRight') }}-->
<!--              </v-btn>-->
            </div>
          </div>
          <div class='_right'>
            <div>
              <img class='oneImg' :src="require('~/assets/images/cloudSales/home/header2-img1.png')" alt='' />
              <img class='oneTwo' :src="require('~/assets/images/cloudSales/home/header2-img2.png')" alt='' />
            </div>
            <img class='oneTree' :src="require('~/assets/images/cloudSales/home/header2-img3.png')" alt='' />
          </div>
        </div>
      </div>
    </div>
    <collaborationMechanism></collaborationMechanism>
    <believeCooperation></believeCooperation>
    <!--全球合作商组件-->
    <!--    <global-partners style='margin-bottom: 16px' />-->
    <!-- 云销售首页组件集合 -->

    <!-- 登录弹窗 type - 0: 个人  1: 企业 -->
    <login-window :type='loginType' @handleCloseLoginDialog='handleCloseLoginDialog' />
  </div>
</template>

<script>
import GlobalPartners from '../components/common/global-partners';

import LoginWindow from '../components/popupWindow/loginWindow.vue';
import collaborationMechanism from '../components/cloudSales/collaborationMechanism.vue';
import believeCooperation from '../components/cloudSales/believeCooperation.vue';
import config from '../config';
import { mapMutations } from 'vuex';
import error from '@/layouts/error';

export default {
  components: {
    GlobalPartners,
    LoginWindow,
    believeCooperation,
    collaborationMechanism
  },
  data() {
    return {
      filterParams: {
        dictionaryType: 1
      },
      // 登录的选项类型
      loginType: -1,
      // 是否显示底部内容
      isShowFooterContent: 0,
      context: '',
      dictionaryContent: {}
    };
  },

  methods: {
    // 滚动事件
    scrollEvent() {
      const oTop = document.body.scrollTop || document.documentElement.scrollTop;
      if (oTop + 50 >= window.screen.height && this.isShowFooterContent === 0) {
        this.isShowFooterContent = 1;
      } else if (oTop + 50 < window.screen.height) {
        this.isShowFooterContent = 0;
      }
    },

    /** 处理登录弹框的关闭操作 */
    handleCloseLoginDialog(value) {
      this.loginType = value;
    },

    handleClick(type) {
      if (type === 1) {
        window.location.href = 'https://play.google.com/store/apps/details?id=com.aioall.waimai&pcampaignid=web_share';
      } else if(type === 2) {
        window.location.href = 'https://apps.apple.com/cn/app/aio-all-in-one/id1451302299';
      }else {
        if (!this.context) {
          this.$message.warning(this.$t('header.placeholder'));
          return;
        }
        window.location.href = '/creation?keywords=' + this.context;
      }
      // window.location.href = '/addressIndex';
    },
    //
    showPosition(position) {
      const latitude = position.coords.latitude;
      const longitude = position.coords.longitude;
    }
  },
  mounted() {
    //获取用户经纬度
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(
        res => {
          console.log(res);
        },
        error => {
          console.log(error);
        }
      );
    } else {
      console.log('Geolocation is not supported by this browser.');
    }


    window.addEventListener('scroll', this.scrollEvent.bind(this));
  }
};
</script>
<style lang='scss'>
.login-input {
  width: 100%;
  height: 52px;
  margin: 30px 0;
  border-radius: 60px;
  background: #ff797c;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 28px;
  color: white !important;
  .el-input__inner{
    background: transparent;
    border: none;
    color:  #FFFFFF;
  }
  .el-input__inner::-webkit-input-placeholder {
    color:  #FFFFFF;
  }
}
</style>
<style scoped lang='scss'>
.customer-collection_footer-close {
  position: fixed;
  right: 5px;
  bottom: 75px;
  z-index: 3;
  width: 24px;
  height: 24px;
}

.head-bg {
  @extend .tran-300ms;
  padding: 120px 0;
  min-height: 800px;
  background: #edf2f6;

  .h-content {
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    position: absolute;

    .h-conte {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: center;
      width: 100%;
      height: 100%;
      flex: 1;

      ._left {
        width: 35%;

        .Business {
          color: #FFF;
          font-size: 16px;
          font-style: normal;
          font-weight: 500;
          line-height: 22px;
          background-color: #254969;
          padding: 4px 16px;
          border-radius: 30px;
          display: inline-block;
        }

        .Services {
          color: #03163B;
          font-size: 56px;
          font-style: normal;
          font-weight: 700;
          line-height: 62px;
          letter-spacing: -1.12px;
          text-transform: capitalize;
          margin-top: .3em;
        }

        .Potential {
          color: #616976;
          font-size: 16px;
          font-style: normal;
          font-weight: 400;
          line-height: 26px
        }

        .button-view {
          margin-top: 20px;
          display: flex;

          .v-btn {
            border-radius: 35px !important;
          }
        }
      }

      ._right {
        .oneImg {
          width: 220px;
        }

        .oneTwo {
          width: 220px;
          margin-left: 16px;
        }

        .oneTree {
          width: 456px;
          margin-top: 20px;
        }
      }
    }
  }
}

/*中屏幕*/
@media screen and(max-width: $big-pc-width) {
  .head-bg .h-content {
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;

    .h-conte {

    }
  }
}

@media screen and (max-width: $pad-max-width) {
  .customer-collection_footer-close {
    display: none;
  }
  .head-bg {
    margin-top: $small-app-bar-height;
    height: 300px;

    .h-content {
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;

      .h-conte {
        ._left {
          width: 35%;


          .Services {
            font-size: 32px;
          }

          .button-view {
            margin-top: 20px;

            .v-btn {
              border-radius: 35px !important;
            }
          }
        }
      }
    }
  }
}


@media screen and (max-width: $pad-max-width) {

}
</style>
