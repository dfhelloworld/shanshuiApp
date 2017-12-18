<template>
  <div class="interactiveService">
        <div class="nav_mark"></div>
        <yd-navbar :title="language.interactiveService.title" fixed>
            <router-link to="/home" slot="left" >
                <span class="back"></span>
            </router-link>
            <!-- <router-link :to="{path:'/s_home',query:{hotelid:hotelid}}" slot="left" v-if="stateFlag == '2'">
                <span class="back"></span>
            </router-link> -->
        </yd-navbar>
         <scroller>
           <section class="community-box">
              <div class="community-list">
                  <ul>
                      <li v-for="item in localshortcutList"   >
                
                          <!-- <router-link :to="{name:item.key, params:{type:item.key}}"> -->
                           <router-link :to="{path:item.linkTo}">
                             	<!-- <img :src="item.imgSrc"> -->
                               <img :src="item.imgSrc" alt="">
                                <!-- <p>{{item.title}}</p> -->
                                 <p>{{item.key}}</p>
                          </router-link>
                      </li>
                  </ul>
              </div>

          </section>
      </scroller>

   
  </div>
</template>
<style>
.community-box {
  width: 100%;
  background: #fff;
}
/* .community-bg{width:100%;height:5rem;background: url("../../assets/images/community-bg.png") center no-repeat;background-size: cover;position: relative;} */
/* button{position:absolute;left:50%;bottom:0;transform:translate(-50%,50%);border: none;width: 6.5rem;height: 1.2rem;background: url("../../assets/images/community-Group@2x.png")center no-repeat;background-size: cover;margin: 0 auto;} */
.community-list {
  width: 100%;
  padding: 2rem 0.3rem 0 0.3rem;
  background: #fff;
  box-sizing: border-box;
  padding-bottom: 0.7rem;
}
.community-list ul {
  overflow: hidden;
}
.community-list li {
  width: 33.33%;
  padding-top: 0.6rem;
  box-sizing: border-box;
  float: left;
  cursor: pointer;
  border-bottom: 1px solid #f4f4f4;
  border-right: 1px solid #f4f4f4;
}
.community-list li:nth-child(3n) {
  border-right: none;
}
.community-list li img {
  height: 1rem;
  margin: 0 auto;
}
.community-list li p {
  text-align: center;
  margin: 0.3rem 0 0.5rem;
  font-size: 0.28rem;
  width: 100%;
  color: #969696;
}
</style>

<script type="text/babel">
import { mapGetters } from "vuex";
import { mapState } from "vuex";
import foot from "../foot.vue";
import menu from "../common/menu.vue";
import guestCenter from "../common/menu/guestCenter.vue";
export default {
  data() {
    return {
      menuFlag: false,
      centerFlag: false,
      shortcutList: [], //按钮组
      serviceList: {},
      localshortcutList:[],
    };
  },
  created: function() {
    //激活菜单
    localStorage.footFlag = 4;
    localStorage.HOTELID = 3;

    this.localshortcutList = [
      {
        key: "orderFood",
        title: "",
        imgSrc: require("../../assets/images/roomservice.png"),
        linkTo: "/orderFood"
      },
      {
        key: "shopping",
        title: "",
        imgSrc: require("../../assets/images/shopping1.png"),
        linkTo: "/shopping"
      },
      {
        key: "maintain",
        title: "",
        imgSrc: require("../../assets/images/plumbing.png"),
        linkTo: "/maintain"
      },
      {
        key: "clean",
        title: "",
        imgSrc: require("../../assets/images/clean.jpeg"),
        linkTo: "/cleanDetail"
      },
      {
        key: "rating",
        title: "",
        imgSrc: require("../../assets/images/rate.png"),
        linkTo: "/rating"
      },
      {
        key: "otherService",
        title: "",
        imgSrc: require("../../assets/images/other.png"),
        linkTo: "/interactiveOther"
      }
    ];

    //获取物业详情
    let params = {
      hotelid: localStorage.HOTELID,
      lang: localStorage.LANGUAGE
    };
    // this.$store.dispatch("getServiceList", params).then(res => {
    //   if (res.code == 0) {
    //     //全部数据
    //     this.serviceList = this.home.data;
    //     console.log(this.hotelDetail);
    //     //重组图标数据
    //     for (var item in this.home.data.shortcutList) {
    //       for (var i in this.localshortcutList) {
    //         if (
    //           this.home.data.shortcutList[item].key ==
    //           this.localshortcutList[i].key
    //         ) {
    //           this.localshortcutList[i].title = this.home.data.shortcutList[
    //             item
    //           ].title;
    //           this.shortcutList.unshift(this.localshortcutList[i]);
    //         }
    //       }
    //     }
    //   } else {
    //     this.$dialog.toast({ mes: res.msg, timeout: 1000 });
    //   }
    // });
  },
  mounted: function() {
    //一级页面falg
    isHomePage(1);
  },
  components: {
    "v-foot": foot,
    "v-menu": menu,
    "v-guestCenter": guestCenter
  },
  computed: {
    ...mapState({
      language: state => state.language.language
    })
  }
};
</script>
