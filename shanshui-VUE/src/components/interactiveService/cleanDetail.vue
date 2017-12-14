<template>
    <div class="serviceSubmit">
        <div class="nav_mark"></div>
        <yd-navbar :title="language.interactiveService.clean" fixed>
            <router-link to="/interactiveService" slot="left">
                <span class="back" ></span>
            </router-link>
        </yd-navbar> 
        
          <section class="community-box">
               <div class="community-list">  
                <yd-cell-group  title="选择服务时间"> 
            <yd-cell-item arrow>
                <span slot="left">服务时间/Time：</span>
                <input type="time"  slot="right"></input>
            </yd-cell-item>
                </yd-cell-group>
                  <br><br>
                <yd-cell-group title="详细信息/Details" class="textarea">
                    <yd-cell-item >
                        <yd-textarea  slot="right" placeholder="请输入信息/Please Type Here" maxlength="200"></yd-textarea>
                    </yd-cell-item>
                </yd-cell-group>


            <br><br> 
                <yd-button size="large" @click.native="submit()" type="primary" shape="circle" class="button">提交/Submit</yd-button>
            </div>
          </section> 
          

    </div>
</template>
<style>
.community-box {
  width: 100%;
  background: #fff;
}
.community-box div {
  overflow: hidden;
}
.community-list {
  width: 100%;
  height: 100%;
  padding: 2rem 0.3rem 0 0.3rem;
  background: #fff;
  box-sizing: border-box;
  padding-bottom: 0.7rem;
  text-align: center;
}
.community-list {
  overflow: hidden;
}
.button {
  bottom: 10%;
}
</style>

<script>
import { mapGetters } from "vuex";
import { mapState } from "vuex"; 
export default {
  data() {
    return {
      tokenSrc: "",
      title: this.$route.params.title,
      flag: 0,
      selected: "",
      options: [],
      message: "",
      datetime1: '',
    };
  },
  created: function() {
    
    let myDate = new Date();
    this.datetime1 = myDate.getHours()+' : ' + myDate.getMinutes();
 
  },
  methods: {
    submit: function() {
      alert("提交成功");
    }
  },
  mounted: function() {
    //一级页面falg
    isHomePage(0);
  },
    computed: {
    ...mapState({
            language: state => state.language.language
        })
    },
};
</script>
