<template>
  <div class="main-page">
    <div class="left-menu" @click.self="onEditNoteEnd()">
      <!-- ノートリスト -->
      <NoteItem
        v-for="note in noteList"
        v-bind:note="note"
        v-bind:key="note.id"
        @delete="onDeleteNote"
        @editStart="onEditNoteStart"
        @editEnd="onEditNoteEnd"
        @addChild="onAddChildNote"
      />

      <!-- ノート追加ボタン -->
      <button class="transparent" @click="onClickButtonAdd">
        <i class="fas fa-plus-square"></i>ノートを追加
      </button>
    </div>
    <div class="right-view" @click.self="onEditNoteEnd()">
      右ビュー
    </div>
  </div>
</template>

<script>
import NoteItem from '@/components/parts/NoteItem.vue'

export default {
  data() {
    return {
      noteList : [],
    }
  },
  methods: {
    onClickButtonAdd : function() {
      this.noteList.push({
        id : new Date().getTime().toString(16),
        name : `新規ノート`,
        mouseover : false,
        editing : false,
        children : [],        
      })
    },
    onDeleteNote : function(parentNote, note) {
      const targetList = parentNote == null ? this.noteList : parentNote.children;
      const index = targetList.indexOf(note);
      targetList.splice(index, 1);
    },
    onEditNoteStart : function(editNote, parentNote) {
      const targetList = parentNote == null ? this.noteList : parentNote.children;
      for (let note of targetList) {
        note.editing = (note.id === editNote.id);
        this.onEditNoteStart(editNote, note);
      }
    },
    onEditNoteEnd : function(parentNote) {
      const targetList = parentNote == null ? this.noteList : parentNote.children;
      for (let note of targetList) {
        note.editing = false;
        this.onEditNoteEnd(note);
      }
    },
    onAddChildNote : function(note) {
      note.children.push({
        id : new Date().getTime().toString(16),
        name : note.name + 'の子',
        mouseover : false,
        editing : false,
        children : [],
      });
    },
  },
  components: {
    NoteItem,
  },
}
</script>

<style scoped lang="scss">
.main-page {
  display: flex;
  height: calc(100vh - 60px);
  .left-menu {
    width: 350px;
    background-color: #f7f6f3;
  }
  .right-view {
    flex-grow: 1;
    padding: 10px;
  }
}
</style>
