<template>
  <div class="maintain">
        <div class="nav_mark"></div>
        <yd-navbar  title="维修/Maintain" fixed>
            <router-link to="/interactiveService" slot="left">
               <span class="back" ></span>
            </router-link>
        </yd-navbar>

 <!-- <section class="community-box"> -->
     <div class="community-list"> 
        <yd-cell-group title="维修列表"> 
             <yd-cell-item arrow v-for="item in list" :href="{ name: 'serviceSubmit', params: { type: item.type, title: item.title }}"  type="link" style="height:50pt"> 
                <img slot="icon" :src="item.img">
                <span slot="left">{{item.title}}</span>
                <span slot="right"></span> 
            </yd-cell-item> 
        </yd-cell-group>
           </div>
 <!-- </section> -->
    </div>
</template>
<<style>
.text{text-align:center}
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
  text-align: center;
}
.community-list {
  overflow: hidden;
}
</style>

<script type="text/babel">
export default {
  data() {
    return {
      page1: 1,
      page2: 1,
      pageSize: 10,
      list: [
        {
          img: require("../../assets/images/airconditioning.png"),
          title: "空调",
          type: 0
        },
        {
          img: require("../../assets/images/plumbing.png"),
          title: "管道",
          type: 1
        },
        {
          img: require("../../assets/images/electrical.png"),
          title: "电器",
          type: 2
        },
        {
          img: require("../../assets/images/furniture.png"),
          title: "家具",
          type: 3
        },
        {
          img: require("../../assets/images/audio.png"),
          title: "媒体",
          type: 4
        },
        {
          img: require("../../assets/images/internet.png"),
          title: "宽带",
          type: 5
        }
      ]
    };
  },

  methods: {
    goNext: function() {
      alert(this.title);
    }
  }
};
</script>