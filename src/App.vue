<script setup>
  import { ref } from 'vue'
  
  const showModal = ref(false)

  function toggleModal(){
    showModal.value = true  
  }
  function closeModal(){
    showModal.value = false
  }

  const newNote = ref("")
  const errorMessage = ref("")
  const notes = ref([])

  function addNote(){
    if(newNote.value.length < 10) {
      return errorMessage.value = "note must be at least 10 characters"
    }
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: new Date
    })
    closeModal()
    newNote.value = ""
    errorMessage.value = ""
  }
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1>Notes App</h1>
        <button @click="toggleModal">+</button>
      </header>
      <div class="board">
        <div class="card" v-for="note in notes" :key="note.id">
          <p class="title">{{note.text}}</p>
          <div class="date">{{note.date.toLocaleDateString("pt-BR")}}</div>
        </div>
      </div>

    <div class="sidebar-modal" v-if="showModal">
      <div class="modal">
        <button class="close" @click="closeModal">X</button>
        <textarea v-model.trim="newNote" name="noteapp" id="noteapp" cols="30" rows="10"></textarea>
        <span>{{errorMessage}}</span>
        <button class="add-note" @click="addNote">Add Note</button>
      </div>
    </div>

    </div>
  </main>
</template>


<style scoped>

  header {
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid rgb(34, 34, 34);
  }

  header h1 {
    color: azure;
    padding-left: 1rem;
  }

  header button {
    width: 60px;
    height: 60px;
    background-color: rgb(14, 201, 154);
    color: rgb(12, 39, 21);
    font-size: 1.8rem;
    cursor: pointer;
  }

  header button:hover {
    background-color: rgb(12, 173, 133);
  }

  .board {
    max-width: 85rem;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 300px);
    place-content: space-between;
    gap: 2rem;
    padding: 1rem;
    margin-top: 2rem;
    position: relative;
  }

  .card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 200px;
    background-color: rgb(14, 201, 154);
    color: black;
    padding: 1.25rem;
  }

  .title {
    color: rgb(12, 39, 21);
    font-size: 1.4rem;
  }

  .date {
    font-weight: bold;
    color: rgb(12, 39, 21);
  }

  .sidebar-modal{
    display: flex;
    justify-content: end;
    transition: all 3s;
  }

  .modal {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    position: absolute;
    top: 70px;
  }

  textarea {
    height: 50vh;
    padding: 1rem;
    font-size: 1rem;
    border: 0;
  }

  .add-note {
    width: 100%;
    height: 60px;
    background-color: #712dcb;
    color: white;
    font-size: 1rem;
    cursor: pointer;
  }

  .modal span {
    color: brown;
  }

  .close {
    width: 60px;
    height: 60px;
    background-color: #712dcb;
    color: white;
    font-size: 1rem;
    cursor: pointer;
  }
</style>