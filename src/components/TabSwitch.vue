<template>
    <div class="yx-supply-list" ref="yxSupplyList" id="yxSupplyList">
        <div class="days-list yunxiang-tap-wrap" @scroll="onScroll">
            <div class="yunxiang-tap-box" :style="{width:widthWrap+'rem'}">
                <div class="yunxiang-tap-item" v-for="subItem of blockData" :key="subItem.id">
                    <span v-if="subItem.tipText" class="tips-value">{{subItem.tipText}}</span>
                    <img class="yunxiang-tap-img" :src="subItem.imageUrl"/>
                    <div class="yunxiang-tap-text">{{subItem.title}}</div>
                </div>
            </div>
            <div class="brand-end-place"></div>
        </div>
        <!-- v-if="activeBarWidthPercent" -->
        <div class="brand-indicator-p" >
            <div class="brand-indicator-container">
                <div class="brand-indicator-cur" :style="{width:activeBarWidthPercent+'%',marginLeft:marginLeftPercent+'%'}"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            blockData:[
                {
                    id:1,
                    imageUrl:require('../assets/image/bean@2x.png'),
                    tipText:'超值',
                    title:'云豆商城'
                },
                {
                    id:2,
                    imageUrl:require('../assets/image/fork@2x.png'),
                    tipText:'85折',
                    title:'云豆商城'
                },
                {
                    id:3,
                    imageUrl:require('../assets/image/huawei@2x.png'),
                    tipText:'82折',
                    title:'华为'
                },
                {
                    id:4,
                    imageUrl:require('../assets/image/jd@2x.png'),
                    tipText:'',
                    title:'京东'
                },
                {
                    id:5,
                    imageUrl:require('../assets/image/mi@2x.png'),
                    tipText:'',
                    title:'小米'
                },
                {
                    id:6,
                    imageUrl:require('../assets/image/mother@2x.png'),
                    tipText:'90折',
                    title:'云豆商城'
                },
                {
                    id:7,
                    imageUrl:require('../assets/image/shose@2x.png'),
                    tipText:'',
                    title:'云豆商城'
                },
                {
                    id:8,
                    imageUrl:require('../assets/image/shwy@2x.png'),
                    tipText:'',
                    title:'云豆商城'
                },
                {
                    id:9,
                    imageUrl:require('../assets/image/sofa@2x.png'),
                    tipText:'',
                    title:'云豆商城'
                },
                {
                    id:10,
                    imageUrl:require('../assets/image/wangyi@2x.png'),
                    tipText:'',
                    title:'网易严选'
                },
                 {
                    id:11,
                    imageUrl:require('../assets/image/sofa@2x.png'),
                    tipText:'',
                    title:'云豆商城'
                },
                {
                    id:12,
                    imageUrl:require('../assets/image/wangyi@2x.png'),
                    tipText:'',
                    title:'网易严选'
                }
            ],
            widthWrap:'',
            contentWidth: 0,//内容的宽度
            containerWidth:'375',//容器的宽度
            activeBarWidthPercent:50,//滑动条占的比例
            marginLeftPercent:0//滑动条偏移距离
        }
    },
    created(){
        this.initData()
    },
    mounted(){
        
    },
    methods:{
        initData(){
            let widthWrap = 0;
            if(this.blockData.length < 9){//一行展示5个商品，展示2行，如果大于10个，宽度也跟着增加
                widthWrap = 750;
            }else{
                if((this.blockData.length %2 == 0)){//如果是偶数，宽度 = 个数 * 150 
                    widthWrap = (this.blockData.length >>1)*150;
                }else{
                    widthWrap = ((this.blockData.length >>1) +1)*150;//如果是基数，宽度 = （个数+1） * 150
                }
            }
            this.widthWrap = widthWrap/100;
            this._syncViewData()
        },
        _syncViewData() {
            let brandContainer = this.$refs.yxSupplyList;
            if (brandContainer) {
                this.containerWidth = brandContainer.offsetWidth * 2;
            }
            this.contentWidth = this.widthWrap * 50 //(50指html font-size 的值)
            if (this.contentWidth > this.containerWidth) {
                this.activeBarWidthPercent = (this.containerWidth / this.contentWidth) * 100;
            }
        },
        onScroll(e){
            let scrollLeft = e.target.scrollLeft;
            if (this.contentWidth) {
                this.marginLeftPercent = (scrollLeft * 100) / this.contentWidth;
            }
        }
    }
}
</script>
<style lang="scss">
.yx-supply-list {
    position: relative;
    height: 3.1rem;
    overflow-x: visible;
    .yunxiang-tap-wrap {
        width: 100%;
        max-width: 414px;
        height: 3.1rem;
        margin:0 auto;
        overflow-x: scroll;
        overflow-y: hidden;
        .yunxiang-tap-box {
            display: flex;
            height: 100%;
            align-items: flex-start;
            flex-wrap: wrap;
            .yunxiang-tap-item {
                position: relative;
                margin: 0.2rem 0.35rem 0;
                width: 0.8rem;
                overflow: visible;
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: center;
                .tips-value {
                    color: #ffffff;
                    font-size: 0.18rem;
                    background: #ff3030;
                    width: 0.6rem;
                    height: 0.32rem;
                    line-height: 0.32rem;
                    text-align: center;
                    position: absolute;
                    top: -0.02rem;
                    left: 0.72rem;
                    border-radius: 0.12rem 0.12rem 0.12rem 0;
                }
                .yunxiang-tap-img {
                    width: 0.8rem;
                    height: 0.8rem;
                }
                .yunxiang-tap-text {
                    color: #333;
                    font-size: 0.22rem;
                    text-align: center;
                    line-height: 0.32rem;
                    margin-top: 0.08rem;
                    font-family: PingFangSC-Regular, PingFang SC;
                    white-space: nowrap; /*强制不换行*/
                }
            }
        }
        .brand-end-place {
            width: 0.3rem;
            height: 0.1rem;
            flex-shrink: 0;
        }
    }
    .brand-indicator-p {
        position: absolute;
        width: 100%;
        height: 0.04rem;
        bottom: -0.1rem;
        left: 0;
        display: flex;
        align-items: center;
        overflow: visible;
        z-index: 100;
        .brand-indicator-container {
            width: 1rem;
            height: 0.04rem;
            background: #d8d8d8;
            border-radius: 0.02rem;
            position: relative;
            overflow: hidden;
            margin: auto;
            .brand-indicator-cur {
                width: 50%;
                height: 0.04rem;
                border-radius: 0.02rem;
                background: #ff8455;
            }
        }
    }
}
</style>
