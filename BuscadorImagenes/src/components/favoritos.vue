<template lang="">
    <div>

<div id="fondo_usuario">
    <div class="cont_usuario">
<div class="img_usuario">
    <img src="https://yt3.ggpht.com/a/AGF-l7-rAaULhpxilaS_PEnH-hSPazPizYUBv4PoOQ=s900-mo-c-c0xffffffff-rj-k-no" alt="">
</div>


    
    <h1>Username</h1>






</div>
</div>






    
<div class="cont_titulo">

    <h1>Su fotos favoritas <i class="fa-solid fa-bookmark "></i></h1>
         
</div>


<div class="cont_favoritos">

<div  v-for="(e, index) in arrayfavs" :key="index"   class="card">

<div class="cont_imagen">
    <div class="div_eliminar">
  
        <a v-on:click="eliminar(index)" class="eliminar" ><i class="fa-solid fa-trash"></i></a>
</div>
   
    <img :src="e.imagen" alt="">
</div>



</div>



</div>


 

    </div>
</template>
<script>
export default {
props: {
    arrayfavs: {
        type: Array,
        required: true
        
    },
},
methods: {
    
eliminar(index){
this.arrayfavs.splice(index,1);

}

},


    
}
</script>
<style scoped >
  

  .cont_header2 {
  
  margin:0 auto;
  width: 70%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: black;
}

.cont_header2 nav ul{
    display: flex;
    align-items: center;

}

.cont_header2 h1{
  display:flex;
  align-items: center;
  color: white;
  padding: 0px;
  font-size: 25px;
 
font-family: 'Oswald', sans-serif;
}


.cont_header2 h1 img{
  width: 70px;
  border-radius: 5em;
}

.cont_header2 nav a{
    transition: all 0.90s;  
    font-size: 20px;
    text-decoration: none;
    color: white;
    font-weight: bold;
    margin: 0 10px;
}


.cont_header2 nav a:hover{
    transition: all 0.90s;
    background-color: #35eb9a;
    color: black;
    padding: 0 10px;
    border-radius: 2em;
}

.ocultar{
    display: none;
}

.mostrar{
display:initial
}


.cont_titulo{

margin: auto;
width: 80%;
text-align: center;
font-size: 25px;

}






.cont_favoritos{
/*background-color: brown;*/
margin: 60px auto;
width: 80%;
display: grid;
grid-template-columns: 1fr 1fr 1fr 1fr ;
gap: 30px;
}

.card{
    text-align: center;
}

.cont_imagen img{
    width: 100%;
    height: 380px;
    border-radius: 15px;
    object-fit: cover;
}

.eliminar{
    color: white; 
    font-size: 50px;
}





.cont_imagen{
    position: relative;
}


.fa-bookmark {
    color: gold;

}


.cont_usuario{
   /* background-color: brown;*/
    margin: 10px auto;
    width: 80%;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    color: white;
}

.img_usuario img{
    width: 100%;
    height: 220px;
    border-radius: 10em;
}

#fondo_usuario{
    background-image: url(https://th.bing.com/th/id/OIP.4XzYb-soDZhDKdeS0iUnQAHaEK?pid=ImgDet&rs=1);
background-repeat: no-repeat;
background-size: cover;
height: 100%;
padding-top: 20px;
padding-bottom: 20px;
}





.div_eliminar{
    transition: all 0.50s;
 opacity: 0;
    position: absolute;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.418);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 380px;
    border-radius: 15px;
}

.div_eliminar:hover{
    opacity: 1;
}

.eliminar{
    transition: all 0.50s;
}

.eliminar:hover{
    transition: all 0.50s;
    color: rgba(212, 0, 0, 0.918);
    cursor: pointer;
}




@media (max-width: 1200px){
    .cont_favoritos{
        grid-template-columns:  1fr 1fr 1fr;
    }
}



@media (max-width:1024px){
    .cont_favoritos{
        grid-template-columns:  1fr 1fr;
    }
}


@media (max-width: 856px){

.cont_favoritos{
    grid-template-columns:  1fr;
}

}





</style>


