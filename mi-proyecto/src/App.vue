<template>
  <my-nabvar></my-nabvar>
  <div class="container my-5">
    <h1 class="text-center mb-4"> Lista de Precios</h1>

    <!-- Iterar categorías -->
    <div v-for="(productos, categoria) in lista" :key="categoria" class="mb-5">
      <h2 class="mb-3 text-primary">{{ categoria }}</h2>

      <div class="row">
        <div
          v-for="(item, index) in productos"
          :key="index"
          class="col-md-4 mb-3"
        >
       <div class="card h-100 shadow-sm">
  <img 
    v-if="item.imagen" 
    :src="item.imagen" 
    class="card-img-top" 
    alt="Imagen de {{ item.nombre }}"
  />
  <div class="card-body">
    <h5 class="card-title">{{ item.nombre }}</h5>
    <p class="card-text text-muted">{{ item.descripcion }}</p>
  </div>
  <div class="card-footer text-end">
    <span class="fw-bold text-success">{{ item.precio }}</span>
  </div>
</div>
        </div>
      </div>
    </div>
  </div>
  <my-footer></my-footer>
</template>

<script>

import MyFooter from '@/components/FooterVue.vue';
import MyNabvar from '@/components/HederView.vue';

export default {
  name: "ListaPrecios",

  components:{
  MyFooter,
 MyNabvar
},
  data() {
    return {
  lista: {
  "Pescados y Mariscos": [
    { nombre: "Centolla 500 grs", descripcion: "Al Vacio sin Glaseo del Seno de Reloncavi", precio: "$12.000", imagen: "" },
    { nombre: "Jaiba 500 grs", descripcion: "Sin Glaseo Solo Carne", precio: "$9.000", imagen: "" },
    { nombre: "Salmon sin Espinas al vacio kg", descripcion: "", precio: "$12.500", imagen: "" },
    { nombre: "Trucha de Rio Arcoiris kg", descripcion: "", precio: "$15.000", imagen: "" },
  ],

  "Conservas Artesanales": [
    { nombre: "Locos Enteros", descripcion: "Machacados y cocidos lt", precio: "$22.500", imagen: "" },
    { nombre: "Locos trozados", descripcion: "Machacados y Cocidos lt", precio: "$19.500", imagen: "" },
    { nombre: "Pulpos", descripcion: "Machacados y Cocidos lt", precio: "$14.500", imagen: "" },
    { nombre: "Lengua de Culenes", descripcion: "Aceite Laurel Pimienta", precio: "$4.500", imagen: "" },
    { nombre: "Picorocos", descripcion: "Aceite Laurel Pimienta", precio: "$4.500", imagen: "" },
    { nombre: "Caracol Locate", descripcion: "Aceite Laurel Pimienta", precio: "$5.200", imagen: "" },
    { nombre: "Erizos", descripcion: "Aceite Laurel Pimienta", precio: "$5.200", imagen: "" },
    { nombre: "Navajuelas", descripcion: "Aceite Laurel Pimienta picor Medio", precio: "$4.200", imagen: "" },
    { nombre: "Piures", descripcion: "Al Natural", precio: "$4.200", imagen: "" },
    { nombre: "Pasta de Salmon", descripcion: "Aceite Laurel Pimienta picor Medio", precio: "$4.700", imagen: "" },
    { nombre: "Pasta de Cholgas", descripcion: "Aceite Laurel Pimienta picor Medio", precio: "$3.300", imagen: "" },
    { nombre: "Pasta de Surtido de Mariscos", descripcion: "Laurel Pimienta Picor Medio", precio: "$3.500", imagen: "" },
    { nombre: "Cholgas Banquete enteras", descripcion: "Aceite Laurel y Pimienta", precio: "$3.300", imagen: "" },
    { nombre: "Choritos Selecionados Esp", descripcion: "Aceite Laurel y Pimienta", precio: "$3.200", imagen: "" },
    { nombre: "Pejerrey", descripcion: "Aceite Laurel y Pimienta Picor Medio", precio: "$3.200", imagen: "" },
    { nombre: "Choro Zapato Rubio", descripcion: "Aceite Pimienta Laurel", precio: "$4.200", imagen: "" },
    { nombre: "Choro Zapato Negro", descripcion: "Aceite Pimienta Laurel", precio: "$4.200", imagen: "" },
  ],

  "Pastas de Ajo": [
    { nombre: "Pasta de Ajo ahumado", descripcion: "120 grs", precio: "$2.900", imagen: "" },
    { nombre: "Pasta de Ajo ahumado Miel", descripcion: "120 grs", precio: "$2.900", imagen: "" },
    { nombre: "Pasta de Ajo ahumado a las Finas Hierbas", descripcion: "", precio: "$2.900", imagen: "" },
    { nombre: "Pasta de Ajo ahumado Merken", descripcion: "", precio: "$2.900", imagen: "" },
    { nombre: "Pasta de Ajo Negro Fermentacion Lenta 30 dias", descripcion: "", precio: "$5.500", imagen: "" },
    { nombre: "Pasta de Ajo Negro Fermentacion Lenta 30 dias Murta", descripcion: "", precio: "$5.500", imagen: "" },
    { nombre: "Pasta de Ajo Negro Fermentacion Lenta 30 dias Maqui", descripcion: "", precio: "$5.500", imagen: "" },
    { nombre: "Concentrado Gotario ajo Negro Fermentacion lenta 30 dias", descripcion: "", precio: "$7.000", imagen: "" },
    { nombre: "Ajo Chilote a Granel", descripcion: "", precio: "$6.000", imagen: "" },
  ],

  "Huevos Gallinas Libres": [
    { nombre: "Huevo Super Extra 65 a 75 grs", descripcion: "Bandeja 30 uni", precio: "$9.000", imagen: "" },
    { nombre: "Huevo Jumbo 76 a 90 grs", descripcion: "Bandeja 20 uni", precio: "$7.800", imagen: "" },
  ],

  "Abejas": [
    { nombre: "Polen pote 200 grs Ulmo", descripcion: "", precio: "$4.000", imagen: "" },
    { nombre: "Miel de Ulmo kg Ralun", descripcion: "", precio: "$5.000", imagen: "" },
    { nombre: "Miel de Tiaca Cochamo", descripcion: "", precio: "$5.500", imagen: "" },
    { nombre: "Cera de abeja kg", descripcion: "Para Carpintero, Zapatero, Cosmetica", precio: "$15.000", imagen: "" },
    { nombre: "Caja Miel y 4 Velas", descripcion: "", precio: "$11.000", imagen: "" },
  ],

  "Quesos y Lacteos": [
    { nombre: "Leche entera Proteina A2", descripcion: "No Reconstituida", precio: "$2.700", imagen: "" },
    { nombre: "Mantequilla 100 crema de leche 250 grs", descripcion: "", precio: "$2.450", imagen: "" },
    { nombre: "Mantequilla Sal rosada 250 grs", descripcion: "", precio: "$2.500", imagen: "" },
    { nombre: "Mantequilla A2 250 grs", descripcion: "", precio: "$3.200", imagen: "" },
    { nombre: "Queso Mantecoso Madurado", descripcion: "", precio: "$8.000", imagen: "" },
    { nombre: "Queso Mantecoso Madurado Oregano", descripcion: "", precio: "$9.500", imagen: "" },
    { nombre: "Queso Mantecoso Madurado Albahaca", descripcion: "", precio: "$9.500", imagen: "" },
    { nombre: "Queso Mantecoso Madurado Merken", descripcion: "", precio: "$9.500", imagen: "" },
    { nombre: "Queso Mantecoso Madurado Llanero", descripcion: "", precio: "$9.000", imagen: "" },
    { nombre: "Queso Parmesano Pasta, Ensaladas y Pizzas", descripcion: "", precio: "$8.000", imagen: "" },
  ],

  "Charcuteria y Cecinas": [
    { nombre: "Longanicilla 250 a 350 grs", descripcion: "Ahumada a leña Reducida en Condimentos", precio: "$3.800", imagen: "" },
    { nombre: "Longaniza 450 gs", descripcion: "Receta de Familia Reducida en grasas a las Finas hierbas Ahumado en Leña 3 uni", precio: "$5.800", imagen: "" },
    { nombre: "Longaniza Campo 400 grs", descripcion: "Receta de Familia Reducida en grasas a las Finas hierbas Ahumado en Leña 4 uni", precio: "$5.600", imagen: "" },
    { nombre: "Chorizo Parrillero 300 grs", descripcion: "Tamaño Justo ChoriPan 4 uni", precio: "$5.400", imagen: "" },
    { nombre: "Longaniza Alemana Salchicha Germana Bratwurst 450 grs", descripcion: "3 uni", precio: "$5.200", imagen: "" },
    { nombre: "Arrollado de Huaso chileno 250 a 300 grs", descripcion: "Con o sin aji", precio: "$5.100", imagen: "" },
    { nombre: "Arrollado Medallon Parrillero 300 grs", descripcion: "Con o sin aji", precio: "$5.100", imagen: "" },
    { nombre: "Pate de Campo Cerdo 150 grs", descripcion: "", precio: "$1.750", imagen: "" },
    { nombre: "Gordas Salchicha Germana 400 grs 4 uni", descripcion: "", precio: "$5.200", imagen: "" },
    { nombre: "Vienesas Artesanles 450 grs", descripcion: "Aprox, Materias Primas Seleccionadas ahumado a leña 6 uni", precio: "$5.100", imagen: "" },
  ],

  "Sales y Aliños": [
    { nombre: "Sal Parrillera Carmenere 450 grs", descripcion: "", precio: "$4.200", imagen: "" },
    { nombre: "Sal Parrillera Cerveza 450 grs", descripcion: "", precio: "$4.200", imagen: "" },
    { nombre: "Sal Parrillera Pimienta 450 grs", descripcion: "", precio: "$4.200", imagen: "" },
    { nombre: "Salmuera Vinagre Manzana 470 ml", descripcion: "", precio: "$7.500", imagen: "" },
    { nombre: "Salmuera humo Miel 470 ml", descripcion: "", precio: "$7.500", imagen: "" },
    { nombre: "Salmuera Merken 470 ml", descripcion: "", precio: "$7.500", imagen: "" },
    { nombre: "Salmuera Finas Hierbas 470 ml", descripcion: "", precio: "$7.500", imagen: "" },
    { nombre: "Salsas para adobar 300 grs Chimichurri", descripcion: "", precio: "$3.700", imagen: "" },
    { nombre: "Salsas para adobar 300 grs barbeque bbq", descripcion: "", precio: "$3.700", imagen: "" },
    { nombre: "Mortero Sal Rosada 3 kg", descripcion: "", precio: "$19.000", imagen: "" },
    { nombre: "Sal Molino 5 Pimientas 65 grs", descripcion: "", precio: "$4.200", imagen: "" },
    { nombre: "Garra de Acero Para Carnes", descripcion: "", precio: "$8.000", imagen: "" },
  ],

  "Pecheras, Bolsos, Mandil y Billeteras": [
    { nombre: "Pechera Reno Café", descripcion: "Porta cuchillo y Bolsillo MultiMuliuso 47x72 cms", precio: "$29.000", imagen: "" },
    { nombre: "Pechera Encerada Reno engresada Café", descripcion: "Porta cuchillo y Bolsillo MultiMuliuso 47x72 cms cuello regulable argolla", precio: "$32.500", imagen: "" },
    { nombre: "Pechera de Cuero Liso Rosada", descripcion: "Bolsillo Multiuso, Porta Cuchillo, Cuello Regulable, Argolla 47x72", precio: "$32.500", imagen: "" },
    { nombre: "Bolso Porta Cuchillo 4 uni Cuero Liso 40x42", descripcion: "", precio: "$23.500", imagen: "" },
    { nombre: "Bolso porta Cuchillo 46uni Cuero Liso 40x46", descripcion: "", precio: "$31.500", imagen: "" },
    { nombre: "Porta Cerveza Manos libres Cuero Liso", descripcion: "", precio: "$12.500", imagen: "" },
    { nombre: "Porta Cerveza Cinturon Cuero Liso Café", descripcion: "", precio: "$12.500", imagen: "" },
    { nombre: "Mandil Bolsillo Multiuso Porta cuchillo, Argolla, 2 Ojetillos Metal 45x55 cms", descripcion: "", precio: "$31.500", imagen: "" },
    { nombre: "Neceser Viajero 22 cms x 10 cms", descripcion: "", precio: "$25.000", imagen: "" },
    { nombre: "Billetera Cuero 4 espacios +1", descripcion: "", precio: "$15.500", imagen: "" },
  ]
}
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}
</style>
