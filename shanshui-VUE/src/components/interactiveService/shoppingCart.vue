<template>
    <yd-layout>
        <div class="nav_mark"></div>
        <yd-navbar :title="language.common.shoppingCart" fixed>
            <div @click="goBack" slot="left">
                <span class="back"></span>
            </div>
        </yd-navbar>

        <section class="promotiom_list top_nav" style="height: 100%">
            <scroller>
                <ul class="type-buy" style="padding-top: 0.5rem">
                    <li v-for="data in cart">
                        <div class="col-4">
                            <img :src="data.pic" alt="">
                        </div>
                        <div class="col-6">
                            <span>{{data.title+" "}}</span>
                            <div class="spinner">
                                <yd-button style="background-color:lightgrey;width:5%" @click.native="changeMoney(data,-1)">-</yd-button>
                                <input type="text" disabled value="" v-model="data.quantity">
                                <yd-button style="background-color:lightgrey;width:5%" @click.native="changeMoney(data,1)">+</yd-button>
                            </div>
                            <ul class="s-price">
                                <li class="col-5">RMB {{data.price*data.quantity}}</li>
                                <yd-button type="danger" style="margin-top:15%" @click.native="removeConfirm(data)">{{language.common.remove}}</yd-button>
                            </ul>
                        </div>
                    </li>
                </ul>
            </scroller>
        </section>


        <!-- 购物车foot -->
        <div class="action-bar">
            <div class="action-btn buy-btn" @click="apply()">{{language.common.submit}}({{ selectedNum }})</div>
            <div class="total">{{language.common.total}}：
                <b>{{ totalPrice | formatMoney }}</b>
            </div>
        </div>
    </yd-layout>
</template>

<style>
.spinner input {
  width: 20%;
  height: 2.5em;
  text-align: center;
}

.spinner a {
  width: 20px;
  font-size: 1.5em;
}
</style>
<script>
import { mapGetters } from "vuex";
import { mapState } from "vuex";
export default {
  data() {
    return {
      dataList: [],
      nextPage: 1,
      noData: false,
      pageFlag: "",
      selectedNum: 0,
      itemQuantity: 1,
      totalPrice: 0,
      cart: []
    };
  },
  created: function() {
    this.pageFlag = this.$route.query.pageFlag;
    if (localStorage.Quantity) {
      this.cart = JSON.parse(localStorage.getItem("cart"));
      this.selectedNum = parseInt(localStorage.Quantity);
      this.totalPrice = parseInt(localStorage.totalPrice);
    }
  },
  filters: {
    formatMoney: function(value) {
      return "￥ " + value.toFixed(2);
    }
  },
  methods: {
    apply: function() {
      this.$dialog.confirm({
        title: "提示",
        mes: "确定购买吗？",
        opts: () => { 
          alert(JSON.stringify(this.cart));

          //   let params = [];
          //   for (var index = 0; index < this.cart.length; index++) {
          //     params[i] = {
          //       hotelid: localStorage.HOTELID,
          //       shoppingid: this.cart[i].id,
          //       token: localStorage.TOKEN,
          //       count: this.cart[i].quantity
          //     };
          //   }
          //   this.$store.dispatch("getShoppingOrder", params).then(res => {
          //     if (res.data.code == 0) {
          //       this.$dialog.toast({
          //         mes: _this.language.msg.buy_info,
          //         timeout: 1000
          //       });
          //       localStorage.c;
          //     } else {
          //       this.$dialog.toast({ mes: res.data.msg, timeout: 1000 });
          //     }
          //   });
          localStorage.Quantity = 0;
          localStorage.totalPrice = 0;
          localStorage.cart = [];
        }
      });
    },

    checkOut: function() {
      // this.$router.push({path:'/shoppingCart'});
    },

    goBack: function() {
      this.$router.go(-1);
    },
    changeMoney: function(item, operation) {
      if (operation < 0) {
        if (item.quantity == 1) {
          return;
        }
        item.quantity--;
        this.totalPrice -= parseInt(item.price);
        this.selectedNum--;
      } else {
        item.quantity++;
        this.totalPrice += parseInt(item.price);
        this.selectedNum++;
      }
    },
    removeConfirm: function(data) {
      this.$dialog.confirm({
        title: "提示",
        mes: "确定移除该物品吗？",
        opts: () => {
          var index = this.cart.indexOf(data);
          if (index > -1) {
            this.cart.splice(index, 1);
            this.selectedNum -= data.quantity;
            this.totalPrice -= data.price * data.quantity;
          }
        }
      });
    }
  },
  mounted: function() {},
  components: {},
  computed: {
    ...mapState({
      language: state => state.language.language
    })
  }
};
</script>