<template>
    <div id="app">
        <div class="title"><p>计算器</p></div>
        <div class="screen">
            <div class="history">
                <div class="item" v-for="item in history" > {{item}}</div>
            </div>
            <div class="input">{{input}}</div>
        </div>
        <div class="btn" >
            <div  v-for="(items, i) in keyboard" class='row'>
                <div :class="{lastline: (i == 4)&&(!j)}"  v-for="(item, j) in items" @click="keydown(i, j)"  class='item'>
                     {{item}} 
                </div>
            </div>
        </div>

        <audio src=''/>
    </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
    data(){
        return{
            keyboard:[
                ['CE','back', ' % ', ' / '],
                ['7','8', '9', ' * '],
                ['4','5', '6', ' - '],
                ['1','2', '3', ' + '],
                ['0','.', ' = ']
            ],
            input: '',
            history:[]
        }
    },
    methods:{
        keydown: function(i, j){
            let key =this.keyboard[i][j];
            this._voice(key.trim());
            if(key != 'CE' && key != 'back' && key.trim() != '='){
                this.input += key;
            }else if(key.trim() == '='){
                let value = eval(this.input);
                if(value){
                    this.history.push(this.input +" = "+ value)
                    this.input = ''
                    setTimeout(() => {
                        this._voice(value);
                    }, 500);
                }
            }else if(key.trim() == 'back'){
                this.input = this.input.substr(0, this.input.length - 1)
            }else if(key.trim() == 'CE'){
                this.input = ''
                this.history = []
            }
        },
        _voice(value){
            if(value){
                if(value > 9){
                    value = value+ "";
                    for(let i = 0; i < value.length; i++){
                        
                        setTimeout(() => {
                            console.log(value[i])
                            this._voice(value[i])
                        }, i * 500);
                    }
                }else{
                    let audio = document.querySelector('audio')
                    if(value == '/'){
                        value = 'chuyi'
                    }else if(value == '.'){
                        value = 'dian'
                    }else if( value == '%'){
                        value = 'chu'
                    }
                    audio.src = '/assets/voice/'+value+'.mp3';
                    audio.play()
                }
            }
        }
    },
    name: "app",
    components: {
    }
};
</script>

<style>

@import url('/font-roboto/fontRoboto.css');
#app {
    font-family: 'Roboto', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #fff;
    margin-top: 60px;
    user-select:none;
}

.title {
    font-weight: 500;
    display:flex;
    
    position: absolute;
    width: 100%;
    height: 47px;
    left: 0;
    top: 0;
    background: #212121;
}
.title > p{
    margin-left: 20px;
}
.screen {
    position: absolute;
    width: 100%;
    left: 0;
    top: 47px;
    bottom: 60%;
    background: #303030;
    display: flex;
    flex-direction:column;
}
.screen > .history{
    display: flex;
    flex: auto;
    overflow: hidden;
    flex-direction: column;
    padding: 5px;
}
.screen > .history> .item{
    display: flex;
    flex-direction: row-reverse;
    align-items: center;
    padding: 3px 0;
}
.screen > .input{
    display: flex;
    flex-direction: row-reverse;
    align-items: center;
    height:50px;
    border-top: 1px solid rgba(255,255,255,0.12);  
    padding: 0 5px;
}

.btn {
    position: absolute;
    width: 100%;
    height: 47px;
    left: 0;
    bottom: 0;
    height: 60%;
    background: #212121;

    display: flex;
    flex-direction:column;
}

.btn > .row{
    height: 25%;
    display: flex;
    justify-content: space-around;
    flex: 1;
}

.btn > .row> .item{
    align-items: center;
    justify-content: center;
    padding: auto 0;
    display: flex;
    background: #212121;
    height: 100%;
    flex: 1;
    margin: auto;
}
.btn > .row> .item:active{
    background: #303030;
}
.btn > .row> .lastline{
    flex: 2;
}


</style>
    
