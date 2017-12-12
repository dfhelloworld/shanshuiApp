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
                     <yd-button type="danger" style="margin-top:15%" @click="remove(data)">{{language.common.remove}}</yd-button>
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
            <div class="total">{{language.common.total}}：<span>¥<b>{{ totalPrice }}</b></span></div>
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
            // getData:function () {
            //     let _this = this
            //     let params = {
            //         hotelid: localStorage.HOTELID,
            //         lang: localStorage.LANGUAGE,
            //         limit:6,
            //         page:_this.nextPage
            //     }
            //     this.$store.dispatch('getShoppingList', params).then(function (res) {
            //         var arrList = res.data.data.list
            //         _this.dataList = _this.dataList.concat(arrList)
            //         _this.nextPage = res.data.data.nextPage
            //     })
            // },
            // infinite:function (done) {
            //     let _this = this
            //     done(true);
            //     if (this.nextPage != '-1') {
            //         _this.getData()
            //     } else {
            //         done(false);
            //         _this.noData = true;
            //     }
            // },
            goDetail:function (id) {
                let data = {};
                for(var key in this.dataList){
                    if (this.dataList[key].id == id){
                        data = this.dataList[key];
                        break;
                    }
                }
                this.saveCart();
                this.$router.push({path:'/buy',query:{info:data,quantity:this.selectedNum}});
            },
            addToCart:function(data){ 
                let _this = this; 
                this.selectedNum ++;
                this.totalPrice += parseInt(data.price);
                var alreadyIndex = this.cart.findIndex(function(item,index){ 
                    return item.id === data.id
                    });  
                if(alreadyIndex==-1){  
                    var cartIndex = this.cart.length;
                    this.cart.push(data);
                    this.$set(this.cart[cartIndex],'quantity',1); 
                    this.saveCart();
                    return;
                }else{   
                    this.cart[alreadyIndex].quantity +=1;
                    this.saveCart();
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
            },
            goBack:function(){
               this.$router.go(-1);
            },
            remove:function(data){
                
            }
        },
        mounted:function () {
            //一级页面falg
            isHomePage(0)
        },
        components: {
        },
    computed: {
    ...mapState({
            language: state => state.language.language
        })
    },

    };
</script>


