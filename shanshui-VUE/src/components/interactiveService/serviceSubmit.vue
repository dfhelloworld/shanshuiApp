<template>
    <div class="serviceSubmit">
        <div class="nav_mark"></div>
        <yd-navbar :title="title" fixed>
            <router-link to="/maintain" slot="left">
                <span class="back" ></span>
            </router-link>
        </yd-navbar> 
        
          <section class="community-box">
               <div class="community-list">  
                <yd-cell-group  title="选择故障和服务时间">
                    <yd-cell-item arrow type="label" class="">
                        <select slot="right"  v-model="selected">
                            <option v-for="option in options" v-bind:value="option.value">
                            {{ option.text }}
                            </option>
                        </select>
                    </yd-cell-item>
 
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
    switch (this.$route.params.type) {
      case 0:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "漏水/Leaking", value: "A" },
            { text: "不制冷/Not Cold", value: "B" },
            { text: "遥控器不工作/Remote Control do not work", value: "C" },
            { text: "其他/Other", value: "D" }
          ]);
        break;
      case 1:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "灯光不亮/Light Broken", value: "A" },
            { text: "冰箱故障/Refrigerator Fault", value: "B" },
            { text: "洗衣机故障/Washing Machine Fault", value: "C" },
            { text: "电磁炉故障/Induction Cooker Fault", value: "D" },
            { text: "微波炉故障/IMicrowave Oven Fault", value: "E" },
            { text: "烤箱故障/Oven Fault", value: "F" },
            { text: "没电/No Power", value: "G" },
            { text: "开关故障/Switch Fault", value: "H" },
            { text: "其他/Others", value: "I" }
          ]);
        break;
      case 2:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "淋浴没有压力/Shower No Pressure", value: "A" },
            { text: "淋浴漏水/Shower Leaking", value: "B" },
            { text: "淋浴排水故障/Shower Drainage Fault", value: "C" },
            { text: "浴缸排水故障/Bathtub Drainage Fault", value: "D" },
            { text: "没有热水/No Hot Water", value: "E" },
            { text: "没有冷水/No Cold Water", value: "F" },
            { text: "面盆故障/Basin Drainage Fault", value: "G" },
            { text: "其他/Others", value: "H" }
          ]);
        break;
      case 3:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "餐桌摇晃/Dining Table Shaky", value: "A" },
            { text: "餐椅摇晃/Dining Chair Shaky", value: "B" },
            { text: "咖啡桌摇晃/Coffee Table Shaky", value: "C" },
            { text: "门故障/Door", value: "D" },
            { text: "窗户故障/Windows", value: "E" },
            { text: "墙面维护/Wall", value: "F" },
            { text: "其他/Others", value: "G" }
          ]);
        break;
      case 4:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "电视频道不清楚，不工作/TV Not Working", value: "A" },
            { text: "DVD不工作/DVD Not Working", value: "B" },
            { text: "遥控器不工作/Remoter do not work", value: "C" },
            { text: "其他/Others", value: "D" }
          ]);
        break;
      case 5:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "打扫房间/Postpone Cleaning", value: "A" },
            { text: "请勿打扫房间/Cancel Cleaning", value: "B" }
          ]);
        break;
      case 6:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "有洗衣/Laundry", value: "A" },
            { text: "换毛巾/Change Tower", value: "B" },
            { text: "收垃圾/Collect Rubbish", value: "C" },
            { text: "整理房间/Make Up Bed", value: "D" }
          ]);
        break;
      case 7:
        (this.selected = "A"),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "电源线以及插线板/Extension Cords", value: "A" },
            { text: "电源转换器/Electrcity Adapter", value: "B" }
          ]);
        break;
      case 8:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "没有宽带/No Internet", value: "A" },
            { text: "宽带太慢/Broadband is too slow", value: "B" }
          ]);
        break;
      case 9:
        (this.selected = 0),
          (this.options = [
            { text: "请选择/Please Choose)", value: 0 },
            { text: "牙刷/Toothbursh", value: "A" },
            { text: "刮胡刀/Razor", value: "B" },
            { text: "棉签/Cotton Swab", value: "C" },
            { text: "针线/Sewing Kit", value: "D" },
            { text: "洗手液/Hand Liquid Soap", value: "E" },
            { text: "洗头液/Shampoo", value: "F" },
            { text: "护发素/Conditioner", value: "G" },
            { text: "浴液/Shower Gel", value: "H" },
            { text: "润肤乳/Bodylotion", value: "I" },
            { text: "卫生袋/Sanitary Bag", value: "J" }
          ]);
        break;
      case 10:
        break;
      default:
        break;
    }
  },
  methods: {
    submit: function() {
      alert("提交成功");
    }
  },
  mounted: function() {
    //一级页面falg
    isHomePage(0);
  }
};
</script>
