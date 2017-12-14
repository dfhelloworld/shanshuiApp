<template> 
    <yd-layout>
        <yd-navbar slot="navbar" title="点餐/Order">
            <router-link to="/interactiveService" slot="left">
                <yd-navbar-back-icon></yd-navbar-back-icon>
            </router-link>
        </yd-navbar>

        <yd-scrolltab style="bottom:55px">
            <yd-scrolltab-panel v-for="item in list" :label="item.label" :icon="item.icon" :active="item.active">
          <ul class="type-buy">
          <li v-for="itm in item.data">
              <div class="col-6">
                  <img  :src="itm.img" alt="">
              </div>
              <div class="col-4">
                  <h4>{{itm.title}}</h4> 
                  <ul class="s-price">
                    <li class="col-6">RMB {{itm.price}}</li>
                    <li class="col-6" style="margin-top:40%"><button type="button" @click="addToCart(itm)">{{language.common.addToCart}}</button></li>
                  </ul>
              </div>
          </li>
        </ul>
            
            </yd-scrolltab-panel>
        </yd-scrolltab> 
             <!-- 购物车foot -->
        <div class="action-bar" > 
            <div class="action-btn buy-btn" @click="checkOut()">{{language.common.shoppingCart}}({{ selectedNum }})</div> 
            <div class="total">{{language.common.total}}：<span>¥<b>{{ totalPrice }}</b></span></div>
        </div>
    </yd-layout> 
</template> 
  <style>  
</style>

<script>
import { mapGetters } from "vuex";
import { mapState } from "vuex";
// import chartfoot from "../chartFoot.vue";
export default {
  data() {
    return {
      list: [
        {
          label: "主食",
          icon: "demo-icons-category1",
          color: "gray",
          data: [{ id:"1",title: "米饭", price: "3" }, {id:"2", title: "面条", price: "4" }]
        },
        {
          label: "小吃",
          icon: "demo-icons-category2",
          color: "blue",
          data: ["麻团", "薯条", "洋葱圈"]
        },
        { label: "甜品", icon: "demo-icons-category3", color: "yellow" },
        { label: "饮品", icon: "demo-icons-category4", color: "green" },
        { label: "炒菜", icon: "demo-icons-category5", color: "saddlebrown" },
        {
          label: "厨师推荐",
          icon: "demo-icons-category6",
          color: "darkgoldenrod"
        }
      ],
        selectedNum:0,
        itemQuantity:1,
        totalPrice:0,
        cart:[]
    };
  },
  created:function () {
      if(localStorage.Quantity){
          this.cart = JSON.parse(localStorage.getItem('cart'));
          this.selectedNum = parseInt(localStorage.Quantity);
          this.totalPrice = parseInt(localStorage.totalPrice);
      }
  },
  mounted: function() {
    
  },
  methods:{
    change : function(){
    },

    addToCart:function(data){  
      let _this = this; 
      _this.selectedNum ++;
      _this.totalPrice += parseInt(data.price);
      var existIndex = _this.cart.findIndex(function(item,index){ 
          return item.id === data.id
      });  
      if(existIndex==-1){  
          var cartIndex = _this.cart.length;
          _this.cart.push(data);
          _this.$set(_this.cart[cartIndex],'quantity',1); 
          _this.saveCart();
          return;
      }else{   
          _this.cart[existIndex].quantity +=1;
          _this.saveCart();
          return;
      }
    },
    checkOut:function(){ 
        this.$router.push({path:'/shoppingCart'});
    },
    saveCart:function(){
        localStorage.setItem('cart',JSON.stringify(this.cart));
        localStorage.setItem('Quantity',parseInt(this.selectedNum));
        localStorage.setItem('totalPrice',parseInt(this.totalPrice)); 
    }
  },
  components: {
    // "v-foot": chartfoot
  },
    computed: {
    ...mapState({
      language: state => state.language.language
    })
  }
};
</script>