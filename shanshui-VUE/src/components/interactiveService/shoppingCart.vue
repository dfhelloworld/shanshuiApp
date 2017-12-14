<template>
  <yd-layout> 
    <yd-navbar :title="language.common.shoppingCart" fixed>
 		<div @click="goBack" slot="left">
			<span class="back" ></span>
		</div>
    </yd-navbar>
   
    <section class="promotiom_list top_nav" style="height: 100%">
      <scroller  >
        <ul class="type-buy" style="padding-top: 0.5rem">
          <li v-for="data in cart">
              <div class="col-4">
                  <img  :src="data.pic" alt="">
              </div>
              <div class="col-6">
                  <span>{{data.title+" "}}X{{" "+data.quantity}}</span> 
                  <ul class="s-price">
                    <li class="col-5">RMB {{data.price}}</li> 
                     <yd-button type="danger" style="margin-top:15%" @click.native="openConfirm(data)">{{language.common.remove}}</yd-button>
                      <!-- <li class="col-6="><yd-spinner max="99" unit="1" v-model="spinner1"></yd-spinner></li> -->
                  </ul> 
                 
              </div>
          </li>
        </ul>
        <!-- <p class="no_data" v-show="noData">{{language.common.noMoreData}}</p> -->
      </scroller>
    </section>

    
    <!-- 购物车foot -->
        <div class="action-bar" > 
            <div class="action-btn buy-btn" @click="apply()">{{language.common.submit}}({{ selectedNum }})</div> 
            <div class="total">{{language.common.total}}： <b>{{ totalPrice | formatMoney }}</b></div>
        </div>
  </yd-layout> 
</template>

<style> 
</style>
<script>
    import { mapGetters } from 'vuex'
    import { mapState } from 'vuex'
    export default {
        data() {
            return {
                dataList: [],
                nextPage: 1,
                noData: false,
                pageFlag:'',
                selectedNum:0,
                itemQuantity:1,
                totalPrice:0,
                cart:[],
                spinner1
            }
        },
        created:function () {
            this.pageFlag = this.$route.query.pageFlag
            if(localStorage.Quantity){
                this.cart = JSON.parse(localStorage.getItem('cart'));
                this.selectedNum = parseInt(localStorage.Quantity);
                this.totalPrice = parseInt(localStorage.totalPrice);
            }
        },
        filters:{
            formatMoney:function(value){
                return "￥ "+ value.toFixed(2);
            }
        },
        methods: {
             apply: function () {
                localStorage.Quantity =0;
                localStorage.totalPrice= 0;
                localStorage.cart = [];
                let _this =this
                let params = [];
                for (var index = 0; index < this.cart.length; index++) {
                     params[i] = {'hotelid':localStorage.HOTELID,'shoppingid':this.cart[i].id,'token':localStorage.TOKEN,'count':this.cart[i].quantity};
                }
                this.$store.dispatch('getShoppingOrder', params).then((res) => {
                	if (res.data.code == 0){
                    	this.$dialog.toast({
                    	    mes: _this.language.msg.buy_info,
							timeout: 1000
                    	});
                        localStorage.c
                    } else {
                    	this.$dialog.toast({mes: res.data.msg, timeout: 1000});
					}
                }) 
			},


            checkOut:function(){ 
                // this.$router.push({path:'/shoppingCart'});

            },

            goBack:function(){
               this.$router.go(-1);
            },
        },
        mounted:function () {

        },
        components: {
        },
    computed: {
    ...mapState({
            language: state => state.language.language
        }),
        openConfirm:function(data) { 
                let _this = this;
                this.$dialog.confirm({
                    title: '提示',
                    mes: '确定移除该物品吗？',
                    opts: () => { 
                        var index =_this.cart.indexOf(data);
                        if(index>-1){
                            _this.cart.splice(index,1);
                            _this.selectedNum -= data.quantity;
                        } 
                        localStorage.setItem('cart',JSON.stringify(_this.cart));
                        localStorage.setItem('Quantity',parseInt(_this.selectedNum));
                        localStorage.setItem('totalPrice',parseInt(this.totalPrice)); 

                    }
                });
            },
    },

    };
</script>


