<script setup>
import { ref } from 'vue'

const showModal = ref(false);
const newNote = ref('');
const errorMessage = ref('');
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";

}

const addNote = () => {
  if (newNote.value.length < 10) {
    return errorMessage.value = 'votre note doit contenir au moins 10 caractères ou plus';
  }
  notes.value.push({
    id:Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgrounColor: getRandomColor()
  })
  showModal.value=false;
  newNote.value='';
  errorMessage.value='';
}

</script>
<template>
  <main>
  <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote()" class="add_modal">Add Note</button>
        <button class="close_modal" @click="showModal=false">Close</button>
      </div>
  </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button class="add" @click="showModal=true">+</button>
      </header>
    <div class="cards-container">

      <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: note.backgrounColor }">
        <p class="main-text">{{ note.text }}</p>
        <p class="date">{{ note.date.toLocaleDateString("fr-FR") }}</p>
      </div>


    </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}

button.add {
border: none;
padding: 10px;
width: 50px;
height: 50px;
cursor: pointer;
background-color:rgb(21,20,20);
border-radius: 100%;
color: white;
font-size: 20px;
}
.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;

}
.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237,182,44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 20px 20px;
} 

.main-text {
  font-size: 15px;
  color: rgb(21,20,20);
}
.date {
  font-size: 12.5px;
  font-weight: bold;
  color: rgb(21,20,20);
}
.overlay {
  position: absolute;
  height: 100%;
  width: 100%;
  background-color: rgba(0,0,0,.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 20px;
}
.add_modal {
  border: none;
  background-color: rgb(237,182,44);
  color: white;
  width: 700px;
  padding: 20px;
  border-radius: 10px;
  margin: 20px;
  cursor: pointer;
}
.close_modal {
  background-color: red;
  color: white;
  width: 700px;
  padding: 20px;
  border-radius: 10px;
  margin: 5px 20px;
  cursor: pointer;
}
#note {
  margin: 20px;
}

.modal p {
  color: red;
  padding: 0 20px;
}
</style>