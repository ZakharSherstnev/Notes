<template>
  <div class="new-note">
    <label for="">Title:</label>
    <input v-model="title" type="text" />
    <label for="">Description:</label>
    <textarea v-model="descr"></textarea>
    <div class="priority">
      <p
        :class="{ active: priority == 'Standard' }"
        @click="priority = 'Standard'"
      >
        Standard
      </p>
      <p
        :class="{ active: priority == 'Important' }"
        @click="priority = 'Important'"
      >
        Important
      </p>
      <p
        :class="{ active: priority == 'Very important' }"
        @click="priority = 'Very important'"
      >
        Very important
      </p>
    </div>

    <button class="btn btnPrimary" @click="store">New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      title: this.note.title,
      descr: this.note.descr,
      priority: this.note.priority,
    };
  },
  methods: {
    store() {
      this.$emit("store", {
        title: this.title,
        descr: this.descr,
        priority: this.priority,
      });
      this.title = "";
      this.descr = "";
      this.priority = "Standard";
    },
  },
};
</script>
<style scoped>
.new-note {
  text-align: center;
  padding: 20px 0;
}
.new-note .btn {
  margin-top: 20px;
}
.priority p {
  padding: 10px;
  display: inline-block;
  margin-top: 20px;
  border: 1px solid #dfdfdf;
  border-radius: 50px;
  margin-left: 10px;
  cursor: pointer;
}
.priority p:first-child {
  margin-left: 0;
}
.active {
  color: #fff;
  background-color: #494ce8;
}
</style>
