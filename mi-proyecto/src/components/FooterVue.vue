<template>
  <footer class="bg-dark text-center text-white">


      <!-- Redes sociales -->
      <section class="mb-4">
        <a class="btn btn-outline-light btn-floating m-1" href="#"><i class="fab fa-facebook-f"></i></a>
        <a class="btn btn-outline-light btn-floating m-1" href="#"><i class="fab fa-google"></i></a>
        <a class="btn btn-outline-light btn-floating m-1" href="#"><i class="fab fa-instagram"></i></a>
      </section>

      <!-- Información de contacto -->
      <section>
        <div class="container text-center text-md-start mt-5">
          <div class="row mt-3">
            <div class="col-md-3 col-lg-4 col-xl-3 mx-auto mb-4">
              <h6 class="text-uppercase fw-bold mb-4"><i class="fas fa-gem me-3"></i>Restaurante</h6>
              <p>Descripción breve o mensaje institucional.</p>
            </div>
            <div class="col-md-4 col-lg-3 col-xl-3 mx-auto mb-md-0 mb-4">
              <h6 class="text-uppercase fw-bold mb-4">Contacto</h6>
              <p><i class="fas fa-home me-3"></i> Puerto Montt, Kito123, Chile</p>
              <p><i class="fas fa-envelope me-3"></i> kito@hotmail.com</p>
              <p><i class="fas fa-phone me-3"></i> + 56921212121</p>
              <p><i class="fas fa-print me-3"></i> + 56931312121</p>
            </div>
          </div>
        </div>
      </section>


    <!-- Copyright -->
    <div class="text-center p-3" style="background-color: rgba(0, 0, 0, 0.2)">
      © 2025 Copyright:
      <a class="text-white" href="/login">Zhuaus</a>
    </div>


    
  </footer>
</template>




<style scoped>
textarea,
input,
select {
  margin-bottom: 10px;
}
.comentario-carousel {
  display: flex;
  overflow-x: auto;
  padding-bottom: 10px;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
}

.comentario-card {
  min-width: 250px;
  scroll-snap-align: start;
  flex-shrink: 0;
  border-radius: 10px;
}

/* Opcional: ocultar scrollbar en algunos navegadores */
.comentario-carousel::-webkit-scrollbar {
  display: none;
}
.comentario-carousel {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>

