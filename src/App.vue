<template>
    <div id="app">
        <div class="title"></div>
        <div class="screen"></div>
        <div class="btn" >
            <div  v-for="(items, i) in keyboard" class='row'>
                <div :class="{lastline: (i == 4)&&(!j)}"  v-for="(item, j) in items" class='item'>
                     {{item}} 
                </div>
            </div>
        </div>
        <!-- <div class="btn"  v-for="item in items" >
              {{ item.message }}
        </div> -->

        
    </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
    data(){
        return{
            keyboard:[
                ['CE','back', '求余', '%'],
                ['7','8', '9', '*'],
                ['4','5', '6', '-'],
                ['1','2', '3', '+'],
                ['0','.', '=']
            ],
            items: [
                { message: 'Foo' },
                { message: 'Bar' }
            ]
        }
    },
    name: "app",
    components: {
        HelloWorld
    }
};
</script>

<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

.title {
  position: absolute;
  width: 100%;
  height: 47px;
  left: 0;
  top: 0;
  background: green;
}
.screen {
  position: absolute;
  width: 100%;
  left: 0;
  top: 47px;
  bottom: 40%;
  background: yellow;
}
.btn {
  position: absolute;
  width: 100%;
  height: 47px;
  left: 0;
  bottom: 0;
  height: 40%;
  background: red;

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
    flex: 1;
    margin: auto;
}
.btn > .row> .lastline{
    flex: 2;
}


</style>
    
