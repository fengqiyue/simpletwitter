<template>
    <div class="item clearfix">
        <div class="item-avatar pull-left">
            <a :href="grapevine.user.url">
                <img :src="grapevine.user.avatarUrl">
            </a>
        </div>
        <div class="avatar-content">
            <div class="content-info">
                <strong><a :href="grapevine.url">{{grapevine.user.name}}</a></strong>
                ·
                <router-link :to="grapevine.id" class="gray">{{grapevine.createdDate}}</router-link>
            </div>
            <div class="content-content">
                <p v-html="grapevine.parsedText"></p>
            </div>
            <div class="content-function">
                <ul class="list-inline mb0 gray">
                    <li>
                        <span class="content-zan" :class="{active:grapevine.isLiked}" @click="zan(grapevine.id)">
                            <i class="fa fa-thumbs-up mr5" aria-hidden="true"></i>
                            <span v-show="grapevine.isLiked">已</span>赞<span v-show="grapevine.isLiked">+1</span>
                        </span>
                    </li>
                    <li>
                        <span class="content-comment" @click="toggleShowComment()">
                            <i class="fa fa-commenting mr4" aria-hidden="true"></i>
                            {{commentNumber}} 评论
                        </span>
                    </li>
                    <li class="dropdown js__content-ops pl0 pr15">
                        <a href="javascript:void(0);" class="dropdown-toggle" data-toggle="dropdown" aria-expanded="false">
                            <i class="fa fa-ellipsis-h" aria-hidden="true"></i>
                        </a>
                        <ul class="dropdown-menu dropdown-menu-left">
                            <li>
                                <a href="" @click.prevent="deleteGrapevine(grapevine.id)">删除</a>
                            </li>
                        </ul>
                    </li>
                </ul>
            </div>
            <comment-list v-show="isShowComment" :thisGrapevine="grapevine" :publishUserText="'楼主'"></comment-list>
        </div>
        
    </div>
   
</template>

<script>
// import commentList from '../../../components/commentList'

export default {
    data(){
        return{
            grapevine:this.item,
            isShowComment:true,
        }
    },
    computed:{
        commentNumber:function(){
            return this.grapevine.comments > 0 ? this.grapevine.comments : '' 
        },
        detailPageUrl:function(){
            return `/2048/${this.grapevine.id}`
        }
    },
    methods:{
        zan:function(id){
            let api = `/api/grapevine/${id}/like${this.grapevine.isLiked ? '/cancel' : ''}`
            $.post(api, {}, (res)=>{
                if(res.status === 0){
                    this.grapevine.isLiked = !this.grapevine.isLiked
                }
                
            })
        },
        deleteGrapevine:function(id){
            let api = `/api/grapevine/${id}/delete`
            $.post(api, {}, (res)=>{
                if(res.status === 0){
                    this.$emit('deleteThisGrapevine',res.data.id)
                }
                
            })
        },
        toggleShowComment:function(){
            this.isShowComment = !this.isShowComment
        }
    },
    props: {
        item: {
            type: Object,
        }
    },
    components:{
        // commentList,
    },
    created:function(){
    },
    mounted:function(){
    }
}

</script>

<style lang="scss" scoped>
    .item{
        padding: 15px 10px;
        background-color: #fff;
        border-bottom: 1px solid #eee;

        img{
            width: 40px;
            border-radius: 50%;
        }
        .avatar-content{
            padding-left: 50px;
        }
        .list-inline{
            >li{
                cursor: pointer;
            }
        }
        .gray{
            color: #999
        }
        .content-content{
            margin-top: 10px;
            margin-bottom: 10px;
        }
        .content-zan{
            &.active{
                color: #009a61;
            }
        }
        .content-comment{
            cursor: pointer;
        }
    }
</style>
