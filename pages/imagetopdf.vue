<template>
  <div id="wrapper">
   <!-- <vue-html2pdf
 
        :show-layout="true"
        
        :enable-download="true"
        :preview-modal="true"
        :paginate-elements-by-height="1400"
        filename="hee hee"
        :pdf-quality="2"
        :manual-pagination="false"
        pdf-format="a4"
        pdf-orientation="portrait"
        pdf-content-width="800px"
 
        @progress="onProgress($event)"
        @hasStartedGeneration="hasStartedGeneration()"
        @hasGenerated="hasGenerated($event)"
        ref="html2Pdf"
    >
        <section slot="pdf-content">
        <canvas height="300" width="300" ref="canv"></canvas>

      
        </section>
    </vue-html2pdf> -->
    <canvas height="300" width="300" id="canv"></canvas>
  </div>
</template>

<script>

export default {
  data(){
    return{
      imag:require("~/static/icon.png")
    }
  },
  mounted(){
    this.loadimg()
  //   this.$refs.html2Pdf.generatePdf()
  },
methods:{
  hasGenerated(){
    console.log('has generated')
  },
  hasStartedGeneration(){
    console.log('started generation')
  },
  onProgress(){
    console.log('on progress')
  },

loadimg(){
var canvas = document.getElementById('canv');
 var ctx = canvas.getContext("2d") ;
var image = new Image();
image.src =this.imag;

image.onload = ()=>{
console.log(image.src)
this.scaleToFit(image.src,canvas, ctx);
} 

}, 

 scaleToFit(img,canvas, ctx){
// get the scale
 var scale = Math.max(canvas.width/img.width, canvas.height/img.height);
 // get the top left position of the image
 var x = (canvas.width/2)-(img.width/2)*scale;
 var  y  =(canvas.height/2)-(img.height/2)*scale; 
    ctx.drawImage(img,x,y, img.width*scale,img.height*scale);
    	console.log(img.height)
 },
}

}
</script>

<style>
#wrapper{
  width:100vw;
  height: 100vh;
  border: 1px solid red;
}

#i3{
 
}
</style>