<script setup>
import {ref} from "vue";

const showModal = ref(false)
const newNote = ref("")
const errorMessage = ref("")
const notes = ref([])

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%";
}

const addNote = () => {
  if (newNote.value.trim().length > 9) {
    notes.value.push({
      id: Math.floor(Math.random() * 10000000),
      text: newNote.value,
      date: new Date(),
      bgcColor: getRandomColor()
    });
    showModal.value = false;
    newNote.value = ""
    errorMessage.value = ""
  } else return errorMessage.value = "Note needs to be 10 characters or more"

}
</script>


<template>
  <main>
<!--  here vif check if true or false to render the element  -->
<!-- vif remove and add the element and vshow just show and hide -->
    <div v-show="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage"> {{ errorMessage }} </p>
        <button @click="addNote">Add Note</button>
        <button @click="showModal = false" class="close">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="card-container">
        <div
            v-for="note in notes"
            :key="note.id"
            class="card"
            :style="{backgroundColor: note.bgcColor}">
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

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 50%;
  color: whitesmoke;
  font-size: 25px;
}

.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 1.5rem;
  margin-bottom: 1.5rem;
  border-radius: 10%;
}

.date {
  font-size: 0.8rem;
  font-weight: bold;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 50%);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;

}

.modal{
  width: 750px;
  background-color: #efefef;
  border-radius: 15px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  border-radius: 5px;
  background-color: #317dbc;
  border: none;
  color: antiquewhite;
  cursor: pointer;
  margin-top: 15px;
}

.modal .close {
  background-color: #ff2e2e;
  margin-top: 10px;
}

.modal p {
  color: red;
}


</style>