<template>
    <div class = "count">
        <div class = "num-box">
            <p>{{h}}</p>
            <p>:</p>
            <p>{{m}}</p>
            <p>.</p>
            <p>{{s}}</p>
        </div>
        <div class = "count-num">
            <button @click = "reset" ref = "reset">计次</button>
            <button class = "start" @click = "start" ref = "start">启动</button>
        </div>
        <div class = "num-time">
            <div class = "box" v-for = "(item,i) in countTime" :key = "i">
                <div class = "number">计次{{item[0]}}</div>
                <div class  = "time">
                    <p>{{item[3]}}</p>
                    <p>:</p>
                    <p>{{item[2]}}</p>
                    <p>.</p>
                    <p>{{item[1]}}</p>
                </div>
            </div>
        </div>
        <div class = "footer">
            <ul>
                <li v-for = "(item,i) in list" :key = "i">{{item}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return{
            h:0,
            m:0,
            s:0,
            list:["🕗","🕗","🕗","🕗"],
            countTime:[],
            num:0,
            flag:true,
            timer:"",
        }
    },
    methods:{
        start() {
            const start = this.$refs.start;
            if(this.flag) {
                start.innerText = "停止";
                start.style.background = "rgba(255,0,0,.6)";
                start.style.color = "#fff";
                start.style.border = "2px solid #ccc";
                this.s = 0;
                this.m = 0;
                this.time();
                this.num++;
                this.flag = false;
            } else{
                start.innerText = "启动";
                start.style.background = "";
                start.style.color = "";
                start.style.border = "";
                setTimeout(() => {
                    clearInterval(this.timer);
                })
                this.count();
                this.flag = true;
            }
        },
        time() {
            this.timer = setInterval (() => {
                this.s++;
                if(this.s >= 60) {
                    this.s = 0;
                    this.m++;
                    if(this.m >= 60) {
                        this.m = 0;
                        this.h++;
                    }
                }
            },17)
        },
        count(){
            this.countTime.push([this.num,this.s,this.m,this.h,]);
        },
        reset() {
            const reset = this.$refs.reset;
            if(this.flag) {
                reset.innerText = "复位";
                reset.style.border = "2px solid #ccc";
                this.flag = false;
            } else{
                reset.innerText = "计次";
                reset.style.border = "";
                this.flag = true;
            }
        }
    },
}
</script>

<style  scoped lang = "scss">
    *{
        margin:0;
        padding:0;
        list-style: none;
        text-decoration: none;
    }
    .count{
        width:100%;
        height:675px;
        background:rgba(0,0,0,);
        position:relative;
        .num-box{
            width:90%;
            height:100px;
            display:flex;
            margin:0 auto;
            p{
                width:20%;
                height:80px;
                font-size:70px;
                line-height:80px;
                color:white;
            }
        }
        .count-num{
            width:90%;
            display:flex;
            justify-content: space-between;
            margin: 30px auto;
            button{
                display:block;
                width:100px;
                height:100px;
                font-size:20px;
                color:#fff;
                border:0;
                background:grey;
                border-radius:100%;
            }
            button:last-child{
                background:rgba(0,255,0,.3);
                color:rgb(0,255,0);
            }
        }
        .num-time{
            width:90%;
            margin:0 auto;
            .box{
               width:100%;
               height:50px;
               display:flex;
               justify-content: space-between;
                .number{
                    width:60px;
                    font-size:16px;
                    line-height:50px;
                    color:#fff;
                }
                .time{
                    width:70px;
                    display:flex;
                    p{
                        line-height:50px;
                        color:#fff;
                    }
                }
            }
        }
        .footer{
            width:100%;
            height:60px;
            position:absolute;
            left:0;
            bottom:0;
            ul{
                display:flex;
                li{
                   
                    width:25%;
                    text-align: center;
                    font-size:40px;
                    line-height:60px;
                }
            }
        }
    }
</style>