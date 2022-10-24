<template>
  <div class="notes">
    <div
      v-for="(note, index) in notes"
      :key="index"
      :class="{ full: !grid }"
      class="note"
    >
      <div class="note-header" :class="{ full__head: !grid }">
        <p style="cursor: pointer" @click="edit = !edit">{{ note.title }}</p>

        <div v-if="edit" class="edit__title">
          <input v-model="note.title" type="text" />
          <button class="btn btnPrimary" @click="edit = !edit">Save</button>
        </div>

        <p class="close" style="cursor: pointer" @click="noteRemove(index)">
          x
        </p>
      </div>
      <div class="note-body">
        <p>{{ note.descr }}</p>
        <span>{{ note.date }}</span>
        <br />
        <span
          class="prior"
          :class="{
            activeImp: note.priority == 'Important',
            activeVery: note.priority == 'Very important',
          }"
        >
          {{ note.priority }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      edit: false,
    };
  },
  methods: {
    noteRemove(index) {
      this.$emit("remove", index);
    },
  },
};
</script>

<style>
.edit__title {
  max-width: 300px;
  display: flex;
}
.edit__title button {
  margin-left: 10px;
  max-height: 55px !important;
}

.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background: #fff;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgpa(0, 0, 0, 0.02);
}
.note:hover {
  box-shadow: 0 30px 30px rgpa(0, 0, 0, 0.04);
  transform: translate(0, -6px);
  transition-delay: 0s !important;
}
.full {
  width: 100%;
  text-align: center;
}
.note-body {
  margin: 20px 0;
}
.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.note-header h1 {
  font-size: 32px;
}
.note-header ._active {
  color: #402caf;
}
.note-header svg {
  margin-right: 12px;
  color: #999;
}
.note-header svg:last-child {
  margin-right: 0;
}
.note-header p {
  color: #402caf;
  font-size: 22px;
}
.note-body span {
  font-size: 14px;
  color: #999;
}
.full__head {
  justify-content: center;
  align-items: center;
}
.full__head .close {
  margin-left: 30px;
}
.full__head .edit__title {
  margin-left: 30px;
}

.activeImp {
  background-color: yellow;
  border-radius: 50px;
  padding: 8px;
}
.activeVery {
  background-color: red;
  border-radius: 50px;
  padding: 8px;
  color: #fff !important;
}
</style>
