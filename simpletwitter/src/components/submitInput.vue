<template>
  <div class="mt20 mb20">
    <form class="clearfix" @blur="hiddenBtn()">
        <input class="form-control"  @focus="showBtn()" placeholder="今天有什么小道消息要发布吗" v-model.trim="submitContent">
        <button v-show="isShowBtn" @click.prevent="submit1024()" class="btn btn-primary pull-right mt10">发布</button>
    </form>
  </div>
</template>

<script>
import bus from '../assets/bus.js'

export default {
    data(){
        return{
            submitContent:'',
            isShowBtn:false,
            userInfo:{},
        }
    },
    computed:{
        userData(){
            return this.$store.state.author
        }
    },
    methods:{
        submit1024:function(e){
            let api = `/api/grapevine/add`
            let data = {'text':this.submitContent}
            $.post(api,data,res=>{
                let  data = Object.assign({user:this.userInfo},{
                        parsedText:this.submitContent,
                        isLiked:false,
                        createdDate:'刚刚',
                        comments:'0',
                        votes:"0"
                        }, res.data)
                bus.$emit('ANew1024',data);
                this.submitContent = ''
            })
        },
        showBtn:function(){
            this.isShowBtn = true
        },
        hiddenBtn:function(){
            this.isShowBtn = false
        }
    },
    created:function(){
        this.$getUserInfo.then(data => this.userInfo = data)
    },
    mounted:function(){
    }
}
</script>

<style lang="scss" scoped>
    form{
        background-color: #fafafa;
        border-bottom: 1px solid #eee;
        padding: 15px 10px;
     
    }
</style>

