<template>

<div>

   <div class="section bg-world px-0 lg:px-1">

     <div class=" ">
       <Navbar />
     </div>


   </div>

   <div class="section dark autospacing ">
     <div class="w-container pt-8">

       <h1>Moon cat viewer</h1>
        <h3>View Guide</h3>
        <p>If you look at your transaction history and view the first transaction you sent; under the input data if you decode the input data you see the catId which you can paste into this site created by a rescuer!</p>
        <button onclick="generateMoonCatImage(document.getElementById('catId').value,10)">Meow</button>
        <input id="catId" type="text" placeholder="Cat Id">
        <br>
            <canvas id="cat-canvas" width="100%"> </canvas>

     </div>
   </div>

 

  <Footer/>

</div>
</template>


<script>
import Navbar from './components/Navbar.vue';
import ZapPanel from './components/ZapPanel.vue';
import Footer from './components/Footer.vue';

import MoonCatTools from '../js/moon-cat-tools.js' 

let moonCatTools = new MoonCatTools()

export default {
  name: 'Home',
  props: [],
  components: {Navbar,ZapPanel,Footer},
  data() {
    return {

    }
  },
  mounted: function () {
      this.generateMoonCatImage('0x0064c9c57b', 2 );
  },
  methods: {
          generateMoonCatImage(catId, size){
            console.log('meow', catId)
            size = size || 10;
            var data = moonCatTools.generateMoonCatImage(catId);
            var canvas = document.getElementById("cat-canvas");
            canvas.width = size * data.length;
            canvas.height = size * data[1].length;
            var ctx = canvas.getContext("2d");


           console.log('meow', data)


            for(var i = 0; i < data.length; i++){
              for(var j = 0; j < data[i].length; j++){
                var color = data[i][j];
                if(color){
                  ctx.fillStyle = color;
                  ctx.fillRect(i * size, j * size, size, size);
                }
              }
            }
          }
  }
}
</script>
