<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="_container">
          <TheMessage v-if="message" :message="message" />
          <TheNewNote @store="store" :note="note" />
          <div class="note-header">
            <h1>{{ title }}</h1>
            <TheSearch
              @search="search = $event"
              :value="search"
              placeholder="Find your note"
            />
            <div class="icons">
              <svg
                style="cursor: pointer"
                :class="{ _active: grid }"
                @click="grid = true"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                style="cursor: pointer"
                :class="{ _active: !grid }"
                @click="grid = false"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>
          <TheNotes @remove="noteRemove" :grid="grid" :notes="notesFilter" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import TheMessage from "./components/TheMessage.vue";
import TheNewNote from "./components/TheNewNote.vue";
import TheNotes from "./components/TheNotes.vue";
import TheSearch from "./components/TheSearch.vue";
export default {
  data() {
    return {
      title: "Notes App",
      search: "",
      message: null,
      grid: true,
      note: {
        title: "",
        descr: "",
        priority: "Standard",
      },
      notes: [
        {
          title: "First Note",
          descr: "Description for first note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "Standard",
        },
        {
          title: "Second Note",
          descr: "Description for second note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "Standard",
        },
        {
          title: "Third Note",
          descr: "Description for third note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "Standard",
        },
      ],
    };
  },
  computed: {
    notesFilter() {
      let array = this.notes,
        search = this.search;
      if (!search) return array;

      search = search.trim().toLocaleLowerCase();

      array = array.filter(function (item) {
        if (item.title.toLocaleLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      return array;
    },
  },
  methods: {
    store(note) {
      let { title, descr, priority } = note;
      if (title === "") {
        this.message = "title can`t be blank!";
        return false;
      }

      this.notes.push({
        title,
        descr,
        priority,
        date: new Date(Date.now()).toLocaleString(),
      });
      this.message = null;
      this.note.title = "";
      this.note.descr = "";
    },
    noteRemove(index) {
      this.notes.splice(index, 1);
    },
  },
  components: { TheMessage, TheNewNote, TheNotes, TheSearch },
};
</script>
