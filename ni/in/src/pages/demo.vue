<template>
    <div>
            <ul class="demo-ul">
                <li v-for="(item,index) in list" :key="index">
                    <div class="title">{{item.title}} <i v-if="item.children.length>0" class="arrow"></i> </div>
                    <div class="content">
                            <div class="item" v-for="(items,indexs) in item.children" :key="indexs">{{items.title}}</div>
                    </div>
                </li>
            </ul>
    </div>
</template>
<script>
export default {
    data(){
        return{
            list:[
                {
                    title:"这是一级",
                    children:[
                        {
                            title:"这是二级"
                        },
                        {
                            title:"这是二级"
                        },
                        {
                            title:"这是二级"
                        },
                        {
                            title:"这是二级"
                        }
                    ]
                },
                 {
                    title:"这是一级2",
                    children:[
                        {
                            title:"这是二级2"
                        }
                    ]
                },
                 {
                    title:"这是一级2",
                    children:[ ]
                },
            ]
        }
    }
}
</script>

<style lang="scss" scoped>
    .demo-ul{
        width: 200px;
        li{
            position: relative;
            .content{
                    display: none;
                    position: absolute;
                    left: 100%;
                    top: 0;
                    width: 200px;
                    border: 1px solid #eee;
            } 
        }
        li:hover .content{
            display: block;
        }
    }

    .arrow{
        display: inline-block;
        width: 6px;
        height: 6px;
        border-top: 1px solid #ccc;
        border-right: 1px solid #ccc;
        transform: rotate(45deg);
    }
</style>