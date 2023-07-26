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
        <i  v-on:click="menu_des()"   class="fa-solid fa-bars "></i>   
        
        <div class="cont_menu_oculto ">
            <a  v-on:click="inicio()"   href="#">Inicio</a>
       <a v-on:click="mostrarfavs()"   href="#">Guardados</a>
       <a href="">Explorar</a>
       <a href="">Licencia</a>
        </div>



<h1 >SEARCHING IMAGES <img src="" alt=""> </h1>

<nav class="nav1"   >
    <ul>

       <a  v-on:click="inicio()"   href="#">Inicio</a>
       <a v-on:click="mostrarfavs()"   href="#">Guardados</a>
       <a href="">Explorar</a>
       <a href="">Licencia</a>
       <a class="img_user"  href=""><img src="https://yt3.ggpht.com/a/AGF-l7-rAaULhpxilaS_PEnH-hSPazPizYUBv4PoOQ=s900-mo-c-c0xffffffff-rj-k-no" alt=""></a>
       
    </ul>
</nav>


   
     
    
   


<!------
<i v-on:click="mostrar_menu()"   class="fa-solid fa-bars menu"></i>
-->
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
      <label > <button  v-on:click=" fetchData()  "  > <i class="fa-solid fa-magnifying-glass"></i></button></label> 
    
    </div>


</div>






<div class="cont_error  ocultar  ">
    <h2>No existen imagenes relacionadas a "{{input_error }}"  </h2>

</div>

<div class="titulo">
<h1>Stock de fotos <i class="fa-solid fa-image"></i></h1>

</div>



<div class="contenedor_imagenes">
    
    <div    class="imagen "   v-for="item in datag" :key="item.id">

<div class="cont_hover "   >

    <a v-on:click="agregar($event)"  ><i class="fa-solid fa-bookmark corazon"></i></a>
    <a v-on:click="mostrar_modal($event)"  ><i class="fa-sharp fa-solid fa-download descargar"></i></a>





</div>


    <img   :src="item.src.landscape"  alt="">
 
    </div>



</div>




</div>

<footer>
<div class="cont_footer">

<h4>@Copyright Pagina Imagedownload </h4>

<a target="blank"  href="https://github.com/Diego03gGomez/BuscadorImagenes">Diego Gomez <i class="fa-brands fa-github"></i></a>


</div>

</footer>


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
let footer = document.querySelector("footer");
footer.classList.add("ocultar")


},
inicio(){
    this.$refs.todo.classList.remove('ocultar');
document.querySelector(".favs").classList.add("ocultar")
let footer = document.querySelector("footer");
footer.classList.remove("ocultar")
},
ocultar_modal(event){
event.currentTarget.parentNode.parentNode.classList.remove("mostrar")

},
mostrar_modal(event){

document.querySelector(".div-pantalla-completa").classList.add("mostrar")
this.img_modal = event.currentTarget.parentNode.parentNode.querySelector("img").src;
},
menu_des(){
   let menu = document.querySelector(".cont_menu_oculto");
   menu.classList.toggle("trasladar")
},





},


mounted () {
    this.fetchData();
},






    
}
</script>







































































<style scoped>

.cont_error{
    text-align: center;color: black;
   
}

.cont_error h2{
   /* padding-top: 40px;*/
  
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0px 0;
    margin: 60px auto;
    width: 50%;
}


.titulo{
    margin:0px auto;
    width: 85%;
    margin-top: 50px;
    margin-bottom: -60px;
    color: black;
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
    width: 85%;
    display: grid;
    grid-template-columns:1fr 1fr 1fr 1fr ;
    gap: 5px;
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

.cont_input input:focus{
outline: none;
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
    color: gold;
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



.cont_header nav a{
    color: black;
    font-size: 25px;
}

.cont_header nav a:not(:last-child):hover{
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


.cont_footer{
  /*  background-color: red;*/
    margin: auto;
    width: 70%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: white;
}

footer{
    background-color: black;
}

.cont_footer a{
    color: white;
    text-decoration: none;
    font-weight: bold;
    font-size: 20px;
}


.img_user img{
width: 100%;
border-radius: 10em;
}

.img_user{
    width: 35px;
}




.nav1 ul{
    font-family: 'Corinthia', cursive;
font-family: 'Fira Sans', sans-serif;
font-family: 'Inter', sans-serif;
font-family: 'Lora', serif;
font-family: 'Mada', sans-serif;
font-family: 'Montserrat', sans-serif;
font-family: 'Mulish', sans-serif;


}

.nav1 ul a{
    font-size: 20px;
}


.nav1 ul {
    align-items: center;
}


.fa-bars {
  display: none;
}

.cont_menu_oculto{
    padding: 5px 0;
    transition: all 0.50s;
   background-color: white;
    position: absolute;
    top: 70px;
    left: 0;
    width: 1%;
    display: flex;
    flex-direction: column;
    text-align: center;
    gap: 30px;
    font-size: 20px;
    font-family: 'Mulish', sans-serif;
    border-radius: 10px;
    opacity: 0;
}

.trasladar{
    transition: all 0.50s;
    opacity: 1;
    width: 100%;
}



.cont_menu_oculto a{
    text-decoration: none;
    color: black;
    background-color: white;
    padding: 10px 0;
    border-radius: 5px;
}

.cont_menu_oculto a:hover{
    background-color: #35eb9a;
    color: black;

}




.cont_header{
    position: relative;
}


.img_user:hover{
    padding: 0;
    transition: all 0.90s;
    background-color: white;
text-align: center;
}

.img_user {
    text-align: center;
}

.btn_descargar{
    color: white;
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
  /*  background-color: red;*/
    width: 80%;
    justify-content: space-around;
    gap: 30px;
}



.cont_header h1{
    font-size: 20px;
}


.cont_input input{
    width: 63%;
}





}


@media (max-width: 800px){
    .nav1{
    display: none;
}

.fa-bars {
    font-size: 20px;
  display: initial;
  cursor: pointer;
}

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
.cont_footer{
    flex-direction: column-reverse;
}


}





    
</style>