<template lang="">
<div>
    <div class=" div-pantalla-completa ocultar">
<div class="header_modal">
    <h1>Imagen completa</h1>


    <i v-on:click="ocultar_modal($event)" class="fa-solid fa-xmark cerrar"></i>

</div>


       

<div class="div_foto">
<img  :src=" img_modal"  alt="">
</div>



    </div>
 
    <!-----
<header>

<div class="cont_header">

<h1>ImageDownload <img  src="../components/imagenes/logo.png" alt=""></h1>

</div>

</header>
--->
<header>
    
    <div class="cont_header">
        <a class="link_oculto"  v-on:click="inicio()"   href="#">Inicio</a>

<h1 >SEARCHING IMAGES <img src="" alt=""> </h1>

<nav class="nav1"   >
    <ul>

       <a  v-on:click="inicio()"   href="#">Inicio</a>
       <a v-on:click="mostrarfavs()"   href="#">Favoritos</a>
       
    </ul>
</nav>


   
     
      <a class="link_oculto"  v-on:click="mostrarfavs()"   href="#">Favoritos</a>
   



<i v-on:click="mostrar_menu()"   class="fa-solid fa-bars menu"></i>

</div>


</header>

<favoritos :arrayfavs=favoritos  class="favs ocultar"  ></favoritos>
<div ref="todo"  id="todo">






<div  id="fondo_input">





    <div class="cont_input">  
        <h1>IMAGEDOWNLOAD</h1>
        <h2>The source of internet images.</h2>
<h2>With resources from creators around the world.</h2>
        <input v-model="valor_input" type="text" placeholder="Buscar imagen">
      <label > <button  v-on:click=" fetchData()  "  >Buscar <i class="fa-solid fa-magnifying-glass"></i></button></label> 
    
    </div>


</div>






<div class="cont_error  ocultar  ">
    <h2>No existen imagenes relacionada a "{{input_error }}"  </h2>

</div>

<div class="contenedor_imagenes">
    
    <div    class="imagen "   v-for="item in datag" :key="item.id">

<div class="cont_hover "   >

    <a v-on:click="agregar($event)"  ><i class="fa-solid fa-heart corazon"></i></a>
    <a v-on:click="mostrar_modal($event)"  ><i class="fa-sharp fa-solid fa-download descargar"></i></a>





</div>


    <img   :src="item.src.landscape"   alt="">
 
    </div>



</div>




</div>


    </div>
</template>
















































<script>

import favoritos from './favoritos.vue';

export default {

    components: {
        favoritos,
    },



    data() {
        return {
            datag: [],
            valor_input : null,
            variable : 0,
           
            favoritos: [
               /* {imagen: "https://th.bing.com/th/id/R.c281b7dae7151ea226119b93ef6ba729?rik=b%2fva9IGmPZEY6Q&pid=ImgRaw&r=0"}*/
            ],
            img_modal: "https://th.bing.com/th/id/R.92a59621de7ddade15c9636540cc0d13?rik=2t415WbRL7f0Ug&pid=ImgRaw&r=0",
input_error : null,
          
        }
    },



methods: {
    async  fetchData() {
  try {
    if(this.valor_input== null) {
    console.log("No hay nada en el input")
 this.variable = 0
} else {
    this.variable = 1;
}

    const apiKey = 'wEZ4U2RKd4dV0euV4iRLVDjY4CZHz3DNJBS5gXXMa2D3FYFjDyFoE66j'; // Reemplaza TU_API_KEY con tu propia clave de API
    const url = `https://api.pexels.com/v1/search?query=${ this.variable == 0 ? "nature" : this.valor_input}&per_page=100`; // URL de la API de Pexels

    const options = {
      headers: {
        'Authorization': apiKey // Incluye la API key en los encabezados de la solicitud
      }
    };



    const response = await fetch(url, options);
    const data = await response.json();
  /*  this.datag = data.photos;
    console.log(data.photos);*/
    if (data.photos.length === 0) {
        console.log("No se encontraron resultados para la búsqueda.");
/*let contenedor = document.querySelector(".contenedor_imagenes");
contenedor.classList.add("ocultar")*/

let error = document.querySelector(".cont_error");
error.classList.add("mostrar");
this.input_error = this.valor_input



      } else {
        this.datag = data.photos;
        console.log(data.photos);
        let errorc = document.querySelector(".cont_error");
errorc.classList.remove("mostrar");

      }
  } catch (error) {
    console.error(error);
   
  }



},




validar(){
    if(this.valor_input === null){
    this.variable = 0
} else{
    this.variable = 1;
}
},

agregar(event){
let img = event.currentTarget.parentNode.parentNode.querySelector("img").src;
console.log(img)
this.favoritos.push({imagen: img})
},

mostrarfavs(){
this.$refs.todo.classList.add('ocultar');
document.querySelector(".favs").classList.remove("ocultar")
},
inicio(){
    this.$refs.todo.classList.remove('ocultar');
document.querySelector(".favs").classList.add("ocultar")
},
ocultar_modal(event){
event.currentTarget.parentNode.parentNode.classList.remove("mostrar")

},
mostrar_modal(event){

document.querySelector(".div-pantalla-completa").classList.add("mostrar")
this.img_modal = event.currentTarget.parentNode.parentNode.querySelector("img").src;
},
mostrar_menu(){
   
    

}




},


mounted () {
    this.fetchData();
},






    
}
</script>







































































<style scoped>

.cont_error{
  
    text-align: center;
}


#fondo_input{
    background:  linear-gradient(to right, #00000059, #00000069, #00000094), url(https://images7.alphacoders.com/108/thumb-1920-1085679.jpg);

    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    height: 70vh;
    display: flex;
  
}













.contenedor_imagenes{
  /*  background-color: brown;*/
    margin:100px auto;
    width: 80%;
    display: grid;
    grid-template-columns:1fr 1fr 1fr 1fr ;
    gap: 20px;
}

.contenedor_imagenes div img{
   
    width: 100%;
    height: 380px;
    object-fit: cover;
    border-radius: 10px;
}

.cont_input{
 
  /* background-color: brown;*/
    margin: 150px auto;
    width: 80%;
    text-align: center;
    color: white;
}

.cont_input h1{
    font-family: 'Corinthia', cursive;
font-family: 'Fira Sans', sans-serif;
font-family: 'Inter', sans-serif;
font-family: 'Lora', serif;
font-family: 'Mada', sans-serif;
font-family: 'Montserrat', sans-serif;
font-family: 'Mulish', sans-serif;
font-family: 'Nunito', sans-serif;
font-family: 'Open Sans', sans-serif;
font-family: 'Oswald', sans-serif;

}



.cont_input input{
    
font-size: 20px;
padding: 9px 10px;
width: 40%;
}

.cont_input button{
  cursor: pointer;
color: white;
background-color: #001c40;
border-style: solid;
border-color: #001c40;
border-radius: 3px;
padding: 10px 20px;
padding-top: 12px;
font-weight: bold;
font-size: 16px;
}
.imagen{
    position: relative;
}



.cont_hover{
    position: absolute;
    background-color: rgba(0, 0, 0, 0.486);
    width: 100%;
    height: 380px;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 30px;
    transition: all 0.90s;
    opacity: 0;
    border-radius: 10px;
}

.cont_iconos{
    background-color: brown;
}



.cont_hover a{
    font-size: 30px;
    color: white;
}





.cont_hover:hover{
    transition: all 0.90s;
    opacity: 1;
    cursor: pointer;
}

.cont_hover:focus{
    transition: all 0.90s;
    opacity: 0;

}

.corazon:hover{
    transition: all 0.35s;
    color: rgba(255, 0, 43, 0.795);
    font-size: 40px;
}
.descargar{
    transition: all 0.35s;
}

.corazon{
    transition: all 0.35s;
}


.descargar:hover{
    transition: all 0.35s;
    color: #35eb9a;
    font-size: 40px;
}




.cont_header nav a:hover{
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
display: initial;
}

.aparecer{
    opacity: 1;
}

.desaparecer{
    opacity: 0;
}





/*ESTILOS PARA LA MODAL*/
.div-pantalla-completa{
    background-color: rgba(0, 0, 0, 0.849);
    color: white;
    position: fixed;
    margin: auto;
    width: 100%;
    height: 100%;
    z-index: 9999;
    padding-top: 100px;
}

.div_foto img{
width: 100%;
height: 600px;
object-fit: cover;
border-radius: 15px;
}

.div_foto{
  /* background-color: brown;*/
    margin: auto;
    width: 70%;
}

.header_modal{
   /* background-color: red;*/
    margin: auto;
    width: 80%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}


.cerrar{
    cursor: pointer;
    font-size: 50px;
}

.menu{
    display: none;
}


.link_oculto{
    display: none;
}




































@media (max-width: 1024px){
    .contenedor_imagenes{
        grid-template-columns: 1fr 1fr 1fr;
    }

.menu{
    display: none;
    font-size: 30px;
    cursor: pointer;
}


.nav1{
    display: none;
}

.link_oculto{
    transition: all 0.30s;
    display: initial;
    text-decoration: none;
    color: black;
    font-size: 25px;
}

.link_oculto:hover{
    transition: all 0.30s;
    background-color:#35eb9a;
    border-radius: 2em;
    padding: 0 5px;
}


.cont_header{
   /* background-color: red;*/
    width: 100%;
    justify-content: center;
    gap: 30px;
    
}

.cont_header h1{
    font-size: 20px;
}


.cont_input input{
    width: 63%;
}



/*
.cont_header nav{
    border-radius: 15px;
   background-color: white;
   position: absolute;
   width: 100%;
   top: 80px;
}

.cont_header nav ul{
    flex-direction: column;
    align-items: center;
}

.cont_header nav ul a{
   
    text-align: center;
   padding: 0 100px;
    margin: 10px 0;
}

.cont_header{
    position: relative;
}*/

}



















































@media (max-width: 768px){

.cont_input{
    width: 90%;
}

.contenedor_imagenes{
        grid-template-columns: 1fr;
    }

#fondo_input{
    height: 100%;
    padding-bottom: 100px;
}


}





    
</style>