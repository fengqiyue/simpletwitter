<template>
    <div class="item-list">
      <item v-for="item in grapevines" :key="item.id" :item="item" @deleteThisGrapevine="deleteA1024"></item>
    </div>
</template>

<script>
import Item from './item.vue'
import bus from '../assets/bus.js'

export default {
	data(){
		return{
			grapevines: [],
		}
	},
	methods:{
		deleteA1024:function(id){
			for(let g in this.grapevines){
				if(this.grapevines[g].id == id){
						this.grapevines.splice(g,1)
				}
			}
		}
	},
	created(){
			bus.$on('ANew1024',(data)=>{
					if(Object.keys(data).length){
							this.grapevines.unshift(data)
					}
			})
	},
	mounted(){
		let api = `/api/grapevine/all`
		$.get(api,res =>{
				this.grapevines = res.data.grapevines;
		})
	},
	
	components:{
			Item
	}
}
</script>

<style lang="scss" scoped>
    
</style>

