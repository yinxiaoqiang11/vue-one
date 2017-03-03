<template>
	<div class="middle" v-if="datas">
		<div class="middle_l" ref="tableft">
			<ul>
				<li v-on:click="click(index)" v-for="item,index in datas" :class="{white:index == getIndex}">
					<div v-bind:class="{active:isActive}">
						<span v-if="item.type>0" :class="mapClass[item.type]">
							
						</span>
						<span>{{item.name}}</span>
					</div>
				</li>
			</ul>
		</div>
		<div class="middle_r" ref="tabright">
			<ul class="mid_wai">
				<li v-for="value in datas" class="food_list">
					<h1>{{value.name}}</h1>
					<ul class="mid_nei">
						<li v-for="items in value.foods">
							<div class="middle_r_l">
								<img v-bind:src=items.image>
							</div>
							<div class="middle_r_r">
								<h2>{{items.name}}</h2>
								<p>{{items.description}}</p>
								<p>
									<span>月售{{items.sellCount}}份</span>
									<span>好评率100%</span>
								</p>
								<div class="mid_r_r_b">
									<div class="zuofu">
										<span>￥28</span>
										<span>￥32</span>
									</div>
									<div class="youfu">
										<span>
											<img src="../../../resource/img/222.png">
										</span>
										<span>1</span>
										<span>
											<img src="../../../resource/img/22.png">
										</span>
									</div>
								</div>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
	</div>
  
</template>
<script>
import BScroll from "better-scroll";
  export default{
  data(){
      return {
       datas:"",
       isActive:true,
       arr:[],
       scrollY:0,
      }
    },
    created(){
      this.mapClass=['decrease','discount','guarantee','invoice','special'];	
      this.$http.get("api/goods")
      .then(function(response){
          return response.json();
      }).then(function(response){
          if(response.success===1){
            this.datas=response.data;
            //$nextTick所有dom节点加载完毕之后，才执行
            this.$nextTick(()=>{
            	this.initBScorll(); 
            	this.tabright.on("scroll",(pos)=>{
            		this.scrollY=Math.abs(Math.round(pos.y));
            	}) ;
            	this.liHeight();
            })
          }
      })
    },
    computed:{
    	getIndex:function(){
    		for(let i=0;i<this.arr.length;i++){
    			let cheight1=this.arr[i];
    			let cheight2=this.arr[i+1];
    			if(this.scrollY>=cheight1&&this.scrollY<=cheight2){
    				return i;
    			}
    			
    		}
    	}
    },
    methods:{
    	click:function(index){
    		let margintop=0;
    		 let ultop=this.$refs.tabright.querySelector(".mid_wai");
    		 let li=this.$refs.tabright.querySelectorAll(".food_list");
    		 let zuoli=this.$refs.tableft.querySelectorAll(".middle_l li");
    		 for(let i=0;i<index;i++){
    		 	margintop+=li[i].offsetHeight;
    		 	zuoli[i].style.backgroundColor="#f3f5f7";
    		 }
    		 ultop.style.marginTop=-margintop+"px";
    		 zuoli[index].style.backgroundColor="white";
    	},
    	initBScorll:function(){
    	this.tableft = new BScroll(this.$refs.tableft,{
          click:true
        });
        this.tabright= new BScroll(this.$refs.tabright,{
          probeType:3
        });
    	},
    	liHeight:function(){
    		let height=0;
    		this.arr.push(height);
    		let li=this.$refs.tabright.querySelectorAll(".food_list");
    		for(let i=0;i<li.length;i++){
    			let liheight=li[i].clientHeight;
    			height+=liheight;
    			this.arr.push(height);
    		}
    	},
    	
    }
    
  }
</script>
<style type="text/css">
	.middle{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		overflow: hidden;
	}
	.middle .middle_l{
		width: 80px;
		background-color: #f3f5f7;
		height:30vh; 	
	}
	.middle .middle_l ul{
		list-style: none;
		background-color: #f3f5f7;	
	}
	.middle .middle_l ul li{
		width:80px;
		height: 54px; 
	}
	.middle .middle_l ul li.white{
		width:80px;
		height: 54px;
		background-color: #fff; 
	}
	.middle .middle_l ul li div{
		width:56px;
		height:53px;
		margin: 0 auto;
		border-bottom:1px solid rgba(7,17,27,0.1);
		line-height:53px;
		font-size: 12px;
		color:#696c70;
		font-weight: 100;   
	}
	.middle .middle_l ul li .active{
		width:56px;
		height: 54px;
		line-height:14px;
		display: table-cell;
		vertical-align: middle;
		position: relative;
		left:12px;
	}
	.middle .middle_l ul li .active span img{
		width:13px;
		height:13px; 
		vertical-align:middle;
	}
	.middle .middle_l ul li .active span img{
		width:13px;
		height:13px; 
		vertical-align:middle;
	}
	.middle .middle_l ul li .active .guarantee{
		background:no-repeat url("../../../resource/img/guarantee_1@2x.png");
		background-size: 13px 13px;
		width: 13px;
		height: 13px;
		display: inline-block;
	}
	.middle .middle_l ul li .active .discount{
		background:no-repeat url("../../../resource/img/discount_1@2x.png");
		background-size: 13px 13px;
		width: 13px;
		height: 13px;
		display: inline-block;
	}
	
	.middle .middle_l ul li div span img{
		width:13px;
		height:13px; 
	}
	.middle .middle_r{
		flex:1;
		height:70vh;
	}
	.middle .middle_r ul{
		list-style: none;
	}
	.middle .middle_r .mid_wai h1{
		height:26px;
		background-color:#f3f5f7;
		color:#cacdd1;
		font-size: 12px;
		line-height: 26px;
		border-left:2px solid #d9dde1; 
		text-indent: 14px;  
	}
	.middle .middle_r .mid_wai .mid_nei{
		list-style: none;
	}
	.middle .middle_r .mid_wai .mid_nei li{
		margin:18px;
		flex-direction: row;
		justify-content:flex-start;
		display: flex; 
		border-bottom:1px solid #d9dde1;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_l{
		width: 58px;
		height:58px;
		margin-right: 10px;
		
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_l img{
		width: 58px;
		height:58px; 
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r{
		flex:1;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r h2{
		color:#07111b;
		font-size: 14px;
		line-height: 14px;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r p{
		font-size: 10px;
		color:#93999f;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r .mid_r_r_b{
		flex-direction: row;
		justify-content:space-between;
		display: flex;
		margin-bottom: 18px; 
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r .mid_r_r_b .zuofu span:nth-child(1){
		color:red;
		font-size: 20px/28px;
		margin-right: 8px;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r .mid_r_r_b .zuofu span:nth-child(2){
		color:#93999f;
		font-size: 10px;
		text-decoration:line-through;
		vertical-align: top;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r .mid_r_r_b .youfu span{
		display: inline-block;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r .mid_r_r_b .youfu span img{
		width: 20px;
		height: 20px;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r .mid_r_r_b .youfu span:nth-child(1){
		width: 20px;
		height: 20px;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r .mid_r_r_b .youfu span:nth-child(2){
		color:#93999f;
		font-size: 10px;
		vertical-align: top;
		line-height: 20px;
		text-align: center;
		width: 20px;
		height: 20px;
	}
	.middle .middle_r .mid_wai .mid_nei li .middle_r_r .mid_r_r_b .youfu span:nth-child(3){
		width: 20px;
		height: 20px;
	}
</style>