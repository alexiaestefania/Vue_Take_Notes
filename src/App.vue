<template>
  <main>
    <div class="modal is-active is-clipped" v-if="showModal">
      <div class="modal-background"></div>
      <div class="modal-card mt-6">
        <header class="modal-card-head has-background-primary is-outlined">
          <p class="modal-card-title has-text-white is-family-sans-serif">
            New note
          </p>
          <button
            class="delete"
            aria-label="close"
            @click="showModal = false"
          ></button>
        </header>
        <section class="modal-card-body">
          <textarea
            class="textarea is-primary is-family-sans-serif"
            name="note"
            id="note"
            cols="30"
            rows="10"
            placeholder="Write your notes here!"
            v-model="newNote"
          ></textarea>
        </section>
        <footer class="modal-card-foot">
          <button @click="addNote" class="button is-success">
            <span class="icon is-small">
              <i class="bi bi-plus is-size-4"></i>
            </span>
            <span class="is-family-sans-serif">Save note</span>
          </button>
        </footer>
      </div>
    </div>
    <nav
      class="navbar is-align-items-center is-primary is-fixed-top has-text-white"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand is-align-items-center">
        <h1 class="ml-2 is-family-primary is-size-2 has-text-left">
          Take Notes!
        </h1>
      </div>
      <div class="navbar-menu ml-2">
        <div class="navbar-start">
          <button
            class="navbar-item button is-family-sans-serif is-primary is-outlined is-inverted is-rounded is-size-6"
            @click="showModal = true"
          >
            <span class="icon is-small is-size-4">
              <i class="bi bi-plus-circle-fill"></i>
            </span>
            <span>New Note</span>
          </button>
        </div>
      </div>
      <div class="navbar-end has-text-white">
        <span class="navbar-item tooltip">
        <i class="bi bi-question-circle"></i>
        <span class="tooltiptext has-background-white-bis has-text-primary is-family-sans-serif is-size-7">
          This is a simple application to take and save notes. 
          Inspired by the app in Laith Academy's 'Ultimate Vue 3 Tutorial' video. 
          The main difference between this app and the one in the video is that I use the local storage to save the notes and display them. 
          As such, the notes will be displayed from the storage, until you clear the browser cache, in which the local sotrage will be emptied.
          Besides that, another difference is the use of Bulma for styling the page, as well as this tooltip.
        </span>
        </span>
      </div>
    </nav>
    <section class="card-container columns section mt-5 is-family-sans-serif is-multiline max-height">
      <div 
      class="card"
      v-for="note in Notes"
      :key="note.id"
      :style="{backgroundColor: note.color}"
      >
        <div class="card-content">
          <div class="content">
            {{ note.text }}
          </div>
        </div>
       
          <time class="card-footer-item"> {{ note.date }}</time>
        
      </div>
    </section>
  </main>
</template>
<style scoped>
@import 'assets/styles/main.scss';
</style>

<script setup>
import { ref } from "vue";

const showModal = ref(false);
const newNote = ref("");
const Notes = ref(JSON.parse(localStorage.getItem('NOTES') ?? '[]'));


const addNote = () => {
  Notes.value.push({
    text: newNote.value,
    date: new Date().toLocaleDateString("pt-BR"),
    id: Math.floor(Math.random() * 99999999),
    color: "hsl(" + Math.random() * 360 + ", 80%, 80%)",
  });
  window.localStorage.setItem('NOTES', JSON.stringify(Notes.value))
  console.log(JSON.parse(localStorage.getItem('NOTES')));
  showModal.value = false;
  newNote.value = "";
};
</script>