<template>
  <div class="rating">
        <div class="nav_mark"></div>
        <yd-navbar  title="评价/Rating" fixed>
            <router-link to="/interactiveService" slot="left">
               <span class="back" ></span>
            </router-link>
        </yd-navbar>

 <!-- <section class="community-box"> -->
     <div class="community-list"> 
        <yd-cell-group title="管家列表"> 
              <yd-accordion>
                  <yd-accordion-item v-for="item in list" :title="item.id+'  '+item.name">
                      <div class="accordionDetail" >
                      <img src="../../assets/images/staff.png" alt=""> 
                          <div style="text-align:center">
                          <yd-rate  style="display:block;margin-top:20px;" v-model="rate"></yd-rate>  
                          <yd-cell-group style="margin-top:10px" title="评价">
                            <yd-cell-item>
                              <yd-textarea slot="right" placeholder="请输入您宝贵的意见" maxlength="200"></yd-textarea>
                            </yd-cell-item>
                          </yd-cell-group>
                          <yd-button size="large" bgcolor="#0099CC" color="white" type="primary" @click.native="submit(item)">提交</yd-button>
                          </div>
                      </div>
                  </yd-accordion-item>
              </yd-accordion>
        </yd-cell-group>
           </div>
 <!-- </section> -->
    </div>
</template>
<<style> 
.accordionDetail{
  height:400px;
  text-align:center;
}
.accordionDetail img{
  width: 50px;
  height: 50px;
  margin:auto;
  margin-top:10px;
  padding:10px,0;
}
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
  padding: 1.5rem 0.3rem 0 0.3rem;
  background: #fff;
  box-sizing: border-box;
  padding-bottom: 0.7rem; 
}
.community-list {
  overflow: hidden;
}
</style>

<script type="text/babel">
export default {
  data() {
    return {  
      list: [
        {
          name: "张三",
          id: "001",
          img: require("../../assets/images/airconditioning.png")
        },
        {
          name: "李四",
          id: "002",
          img: require("../../assets/images/airconditioning.png")
        },
        {
          name: "王五",
          id: "003",
          img: require("../../assets/images/airconditioning.png")
        },
        {
          name: "赵六",
          id: "004",
          img: require("../../assets/images/airconditioning.png")
        },
        {
          name: "周正",
          id: "021",
          img: require("../../assets/images/airconditioning.png")
        },
        {
          name: "小丽",
          id: "123",
          img: require("../../assets/images/airconditioning.png")
        }
      ],
      rate:0,
      comment:"",
      
    };
  },

  methods: {
    goNext: function() {
      alert(this.title);
    }
  }
};
</script>