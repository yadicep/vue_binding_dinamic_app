<script>
  import imgRegular from '/src/assets/img/regular.png';
  import imgBien from '/src/assets/img/bien.png';
  import imgMuyBien from '/src/assets/img/muyBien.png';
  import imgIncreible from '/src/assets/img/increible.png';
  import 'bootstrap/dist/css/bootstrap.min.css';
  import 'bootstrap';
  import Dropdown from 'bootstrap/js/dist/dropdown';

  export default {
    name: "App",
    data() {
      return {
        titulo: "FrontEnd",
        apreciacion: "",
        competencias: [],
        opinion: "",
        emojies: [
        { name: "Regular", src: imgRegular },  
        { name: "Bien", src: imgBien },
        { name: "Muy Bien", src: imgMuyBien },
        { name: "Increible", src: imgIncreible }
      ],  
      selectedEmoji: "", 
      };
    },
    methods: {
      selectEmojiOption(emoji) {
        this.selectedEmoji = emoji.src;
        const dropdownElement = document.getElementById('dropdownMenuButton');
        const dropdownInstance = Dropdown.getInstance(dropdownElement) || new Dropdown(dropdownElement);
        dropdownInstance.hide();
      },
    }
  };
</script>

<template>
  <div id="app">
    <form>
      <!-- TITULO -->
      <div class="p-0 m-0">
          <label class="form-label">Título: </label>
          <input type="text" class="form-control" v-model="titulo">
      </div>
      <hr class="p-0 m-0">
      <!-- EMOJI -->
      <div class="p-0 m-0">
        <label class="form-label">Emoji:</label>
        <div class="dropdown">
          <button class="btn btn-secondary dropdown-toggle" :class="{'dropdown-button': !selectedEmoji}" type="button" id="dropdownMenuButton" data-bs-toggle="dropdown" aria-expanded="false">
            <img v-if="selectedEmoji" :src="selectedEmoji"  height="20px" width="20px"/>
          </button>
          <ul class="dropdown-menu dropdown-menu-dark" aria-labelledby="dropdownMenuButton">
            <li v-for="emoji in emojies" :key="emoji.name" @click="selectEmojiOption(emoji)" class="dropdown-item">
              <img :src="emoji.src" :alt="emoji.name" height="20px" width="20px"/>
            </li>
          </ul>
        </div>
      </div>
      <hr class="p-0 m-0">
      <!-- APRECIACIÓN -->
      <div class="p-0 m-0 form-check">
          <label class="form-label">Apreciación: </label>
          <div class="form-check form-check-inline">
              <input class="form-check-input" type="radio" name="apreciacion" value="Regular" v-model="apreciacion">
              <label class="form-check-label">Regular </label>
          </div>
          <div class="form-check form-check-inline">
              <input class="form-check-input" type="radio" nname="apreciacion" value="Bien" v-model="apreciacion">
              <label class="form-check-label">Bien </label>
          </div>  
          <div class="form-check form-check-inline">
              <input class="form-check-input" type="radio" name="apreciacion" value="Muy Bien" v-model="apreciacion">
              <label class="form-check-label">Muy bien </label>
          </div>
          <div class="form-check form-check-inline">
              <input class="form-check-input" type="radio" name="apreciacion" value="Increíble" v-model="apreciacion">
              <label class="form-check-label">Increíble </label>
          </div> 
      </div>
      <hr class="p-0 m-0">
      <!-- COMPETENCIAS APRENDIDAS -->
      <div class="text-start p-0 m-0">
        <label class="form-label">Competencias<br>aprendidas: </label>
        <ul class="sinPuntos p-1">
          <li><input type="checkbox" value="Morfología de un componente" v-model="competencias" name="competencias"/>Morfología de un componente</li>
          <li><input type="checkbox" value="One-Way y Two-Way data binding" v-model="competencias" name="competencias"/>One-Way y Two-Way data binding</li>
          <li><input type="checkbox" value="El patrón de diseño MVVM" v-model="competencias" name="competencias"/>El patrón de diseño MVVM</li>
        </ul>
        <ul class="sinPuntos p-1">
          <li><input type="checkbox" value="Directivas" v-model="competencias" name="competencias"/>Directivas</li>
          <li><input type="checkbox" value="Estado" v-model="competencias" name="competencias"/>Estado</li>
        </ul>
      </div>
      <hr class="p-0 m-0">
      <!-- OPINIÓN -->
      <div>
          <label class="form-label">Opinión: </label>
          <textarea class="form-control" rows="3" v-model="opinion"></textarea>
      </div> 
    </form> 
    <!-- MOSTRAR DATOS DINÁMICAMENTE -->
    <div class="carnet text-center p-5">
        <div v-if="selectedEmoji">
          <img :src="selectedEmoji" height="50px" width="50px">
        </div>
        <div v-else>
          <p><small>¿Qué te parece este curso?</small></p>
        </div><br>
        <h1>Estoy aprendiendo <span>{{titulo}}</span></h1>
        <p class="h5 fw-bold">Y me parece <span>{{ apreciacion }}</span></p><br>
        <p class="h6 fw-bold">He aprendido:</p>
        <span class="fs-6">{{ competencias.join(', ') }}</span><br>
        <p class="h6 fw-bold">Mi opinión hasta ahora del framework es: </p>
        <span class="fs-6">{{ opinion }}</span>
    </div>
  </div>
</template>

<style scoped>
  form {
      width: 520px;
      padding: 18px;
      border-radius: 12px;
      border: 1px;
      box-shadow: 2px 2px 2px 2px gray;
      font-weight: bold;
      display: flex;
      flex-direction: column;
      gap: 15px;
      background-color: black;
      color: rgb(136, 136, 137);
      font-weight: 300;
  }

  form div {
      display: flex;
      align-items: left;
      gap: 5px;
  }

  .sinPuntos li{
    display: flex;
    justify-content: left;
  }

  .carnet {
      width: 780px;
      height: 450px;
      background: white;
      color: black;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 2px 2px 2px 2px gray;
      display: flex;
      flex-direction: column;
  }

  .dropdown-button {
  background-image: url('/src/assets/img/regular.png'); 
  background-repeat: no-repeat;
  background-position: left;
  padding-left: 50px; 
  background-position: 27%;
  background-size: 20px 20px; 
}

</style>
