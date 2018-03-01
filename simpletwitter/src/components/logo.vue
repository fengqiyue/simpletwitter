<template>
    <router-link to="/">
        <div class="logo clearfix">
        
            <div class="clearfix pull-left">
                <div class="pull-left ml15">
                    <h4>SimpleTwitter</h4>
                    <p>有趣的小道消息</p>
                </div>
            </div>
        
        </div>
    </router-link>
</template>

<script>
export default {
  data(){
      return {

      }
  },
  methods:{
 
  },
  mounted:function(){
	}
}
</script>

<style lang="scss" scoped>
    .logo{
        text-align: center;
        margin-top: 30px;        
        >div{
            position: relative;
            left: 50%;
            transform: translateX(-50%);
        }
        h4{
            font-size: 24px;
            color: #212121;
            font-weight: bold;
        }
        p{
            color: #999;
            font-size: 14px;
            margin-bottom: 0;
        }
    }

</style>

