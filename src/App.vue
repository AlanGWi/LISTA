<template>
  <div id="app">
    <my-nabvar></my-nabvar>

    <main class="flex-grow-1">
      <div class="container my-5">
        <h1 class="text-center mb-4">Lista de productos</h1>

        <!-- Categorías -->
        <div v-if="!categoriaSeleccionada" class="row">
          <div 
            v-for="(productos, categoria) in lista" 
            :key="categoria" 
            class="col-md-4 mb-4"
          >
            <div class="card h-100 shadow-sm" @click="seleccionarCategoria(categoria)" style="cursor: pointer;">
              <img 
                v-if="imagenesCategorias[categoria]" 
                :src="imagenesCategorias[categoria]" 
                class="card-img-top img-fixed" 
                :alt="categoria"
              />
              <div class="card-body text-center">
                <h5 class="card-title">{{ categoria }}</h5>
              </div>
            </div>
          </div>
        </div>

        <!-- Productos de categoría -->

        
        <div v-else>

          <nav aria-label="breadcrumb" class="mb-3">
  <ol class="breadcrumb">
    <li class="breadcrumb-item">
      <a href="#" @click.prevent="categoriaSeleccionada = null">Categorías</a>
    </li>
    <li class="breadcrumb-item active" aria-current="page">
      {{ categoriaSeleccionada }}
    </li>
  </ol>
</nav>

         
          <h2 class="mb-3 text-primary">{{ categoriaSeleccionada }}</h2>

          <div class="row">
            <div
              v-for="(item, index) in lista[categoriaSeleccionada]"
              :key="index"
              class="col-md-4 mb-3"
            >
              <div class="card h-100 shadow-sm">
                <img 
                  v-if="item.imagen" 
                  :src="item.imagen" 
                  class="card-img-top img-fixed" 
                  :alt="item.nombre"
                />
                <div class="card-body">
                  <h5 class="card-title">{{ item.nombre }}</h5>
                  <p class="card-text text-muted">{{ item.descripcion }}</p>
                </div>
                <div class="card-footer text-end">
                  <span class="fw-bold text-success">{{ item.precio }}</span>
                </div>
                 <button class="btn btn-sm btn-primary ms-2" @click="agregarAlCarrito(item)">
            Agregar carrito
          </button>
              </div>
          </div>


    <div>
    <!-- Botón flotante del carrito -->
    <button 
      class="btn btn-primary rounded-circle position-fixed"
      style="bottom: 20px; right: 20px; width: 60px; height: 60px; font-size: 24px;"
      data-bs-toggle="modal" 
      data-bs-target="#carritoModal"
    >
      🛒
      <!-- Badge de cantidad -->
      <span 
        v-if="carrito.length" 
        class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger"
        style="font-size: 14px;"
      >
        {{ carrito.length }}
      </span>
    </button>

    <!-- Modal del carrito -->
    <div class="modal fade" id="carritoModal" tabindex="-1" aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">🛒 Tu carrito</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
          </div>
          <div class="modal-body">
            <ul v-if="carrito.length" class="list-group mb-3">
              <li 
                v-for="(p, i) in carrito" 
                :key="i" 
                class="list-group-item d-flex justify-content-between align-items-center"
              >
                {{ p.nombre }}
                <span class="text-success fw-bold">{{ p.precio }}</span>


                  <button 
              class="btn btn-danger btn-sm" 
              @click="eliminarDelCarrito(i)"
            >
              🗑
            </button>
              </li>
            </ul>



                   <!-- Nueva sección: Envío o Retiro -->
        <div v-if="carrito.length" class="mt-3">
          <h6 class="fw-bold">📦 Método de entrega</h6>
          <div class="form-check">
            <input 
              class="form-check-input" 
              type="radio" 
              id="retiro" 
              value="retiro" 
              v-model="metodoEntrega"
            >
            <label class="form-check-label" for="retiro">
              Retiro en local
            </label>
          </div>
          <div class="form-check">
            <input 
              class="form-check-input" 
              type="radio" 
              id="envio" 
              value="envio" 
              v-model="metodoEntrega"
            >
            <label class="form-check-label" for="envio">
              Envío a domicilio
            </label>
          </div>
          </div>

            
            <p v-else class="text-center">Tu carrito está vacío</p>
          </div>
          <div class="modal-footer" v-if="carrito.length">
            <button class="btn btn-success w-100" @click="enviarCarritoWhatsApp">
              Enviar pedido por WhatsApp
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
      
             <button class="btn btn-secondary mb-4" @click="categoriaSeleccionada = null">
            Volver a categorías
          </button>
            </div>
        </div>

      </div>
    </main>

    <my-footer></my-footer>
  </div>
</template>
<script>
import MyFooter from '@/components/FooterVue.vue';
import MyNabvar from '@/components/HederView.vue';

export default {
  name: "ListaPrecios",
  components: { MyFooter, MyNabvar },
data() {
  return {
    categoriaSeleccionada: null,
    lista: {}, // Se llenará con los productos desde Google Sheets
    imagenesCategorias: {}, // Se llenará con la otra hoja
    carrito: [] ,  // ✅ Aquí inicializas el carrito
    metodoEntrega: "" 
  };
},
mounted() {
  this.cargarDatos();
},
methods: {

eliminarDelCarrito(index) {
    this.carrito.splice(index, 1);
  },


    agregarAlCarrito(item) {
    this.carrito.push(item)
  },
  enviarCarritoWhatsApp() {
    if (!this.carrito.length) {
      alert("Tu carrito está vacío")
      return
    }


      if (!this.metodoEntrega) {
    alert("⚠️ Por favor selecciona si quieres Retiro o Envío.");
    return;
  }

    // Texto con productos
    const productosTexto = this.carrito
      .map(p => `${p.nombre} - ${p.precio}`)
      .join("%0A") // %0A = salto de línea en URL

    // Total
    const total = this.carrito.reduce((sum, p) => {
      const precio = parseInt(p.precio.replace(/\D/g, "")) || 0
      return sum + precio
    }, 0)

    // Mensaje final
     const mensaje = `Nuevo pedido:%0A${productosTexto}%0A%0ATotal: $${total}%0AEntrega: ${this.metodoEntrega === 'envio' ? 'Envío a domicilio' : 'Retiro en local'}`;

    // Número destino (cambia con código país, ej: Chile +56)
    const numero = "+56984415834"

    const url = `https://wa.me/${numero}?text=${mensaje}`
    window.open(url, "_blank")
  },
  async cargarDatos() {
    try {
      // URL pública de tus hojas en formato CSV
      const urlProductos = "https://docs.google.com/spreadsheets/d/e/2PACX-1vRxcOW3Hgc-AhzNqZ_sAZ_Mssov8PCHPTqBeRxxzKeNMbY6YGlT2Jy5K1FBTWhEXL6iN_0QdPzIv8yO/pub?output=csv&t="+ Date.now();
      const urlCategorias = "https://docs.google.com/spreadsheets/d/e/2PACX-1vQFKecgjBfBjTE9wNMzSfevo-wzMn50dv2YPdGQ5LPuK0UFc1xKHXSHGUutkQVs4lHU9RfVKltaheu1/pub?gid=0&single=true&output=csv&t="+ Date.now();

      // 1. Obtener productos
      const resProd = await fetch(urlProductos);
      const textProd = await resProd.text();
      this.lista = this.parseCSVProductos(textProd);

      // 2. Obtener categorías (imágenes)
      const resCat = await fetch(urlCategorias);
      const textCat = await resCat.text();
      this.imagenesCategorias = this.parseCSVCategorias(textCat);

    } catch (error) {
      console.error("Error cargando datos de Google Sheets:", error);
    }
  },

  // Convierte CSV de productos en objeto { categoria: [items] }
parseCSVProductos(csv) {
  const rows = csv.split("\n").map(r => r.split(","));
  const data = rows.slice(1);

  const lista = {};
  data.forEach(row => {
    if (row.length < 5) return; // evitar filas vacías
    const categoria = row[0].trim();
    const nombre = row[1].trim();
    const descripcion = row[2].trim();
    const precio = row[3].trim();
    const imagen = row[4].trim();

    if (!lista[categoria]) lista[categoria] = [];
    lista[categoria].push({ nombre, descripcion, precio, imagen });
  });
  return lista;
},

  // Convierte CSV de categorías en objeto { categoria: urlImagen }
parseCSVCategorias(csv) {
  const rows = csv
    .split("\n")
    .map(r => r.split(","))
    .filter(row => row.length >= 2); // Ignorar filas que no tengan al menos 2 columnas

  // Ignorar headers si es que tu CSV tiene fila de títulos
  const data = rows.slice(1);

  const categorias = {};
  data.forEach(row => {
    const categoria = row[0]?.trim();
    const imagen = row[1]?.trim();
    if (categoria && imagen) {
      categorias[categoria] = imagen;
    }
  });

  return categorias;
},

  seleccionarCategoria(categoria) {
    this.categoriaSeleccionada = categoria;
  }
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


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}


#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh; /* ocupa toda la altura de la pantalla */
}

main.flex-grow-1 {
  flex: 1 0 auto; /* crece para empujar el footer abajo */
}

.img-fixed {
  width: 100%;
  height: 200px; /* ajusta a la altura que quieras */
  object-fit: cover; /* recorta y mantiene proporción */
  border-radius: 8px; /* opcional: bordes redondeados */
}


my-footer {
  flex-shrink: 0; /* nunca se encoge */
}

</style>
