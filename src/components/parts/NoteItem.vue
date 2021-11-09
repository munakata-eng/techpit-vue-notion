<template>
  <div class="note-family">
  <div class="note"
    @mouseover="onMouseOver"
    @mouseleave="onMouseLeave"
    v-bind:class="{mouseover: note.mouseover && !note.editing}"
  >
    <template v-if="note.editing">
      <input v-model="note.name" class="transparent" @keypress.enter="onEditEnd" />
    </template>
    <template v-else>
    <div class="note-icon">
      <i class="fas fa-file-alt"></i>
    </div>
    <div class="note-name">{{note.name}}</div>

    <div v-show="note.mouseover" class="buttons">
      <div class="button-icon" v-if="layer < 3" @click="onClickChildNote(note)">
        <i class="fas fa-sitemap"></i>
      </div>
      <div class="button-icon" @click="onClickAddNoteAfter(parentNote, note)">
        <i class="fas fa-plus-circle"></i>
      </div>
      <div class="button-icon" @click="onClickEdit(note)">
        <i class="fas fa-edit"></i>
      </div>
      <div class="button-icon" @click="onClickDelete(parentNote, note)">
        <i class="fas fa-trash"></i>
      </div>
    </div>
    </template>
  </div>
  <div class="child-note">
    <draggable v-bind:list="note.children" group="notes">
    <NoteItem
      v-for="childNote in note.children"
      v-bind:note="childNote"
      v-bind:parentNote="note"
      v-bind:layer="layer + 1"
      v-bind:key="childNote.id"
      @delete="onClickDelete"
      @editStart="onClickEdit"
      @editEnd="onEditEnd"
      @addChild="onClickChildNote"
      @addNoteAfter="onClickAddNoteAfter"
    />
    </draggable>
  </div>
  </div>  
</template>

<script>
import draggable from 'vuedraggable'
export default {
  name: 'NoteItem',
  props: [
    'note',
    'parentNote',
    'layer',
  ],
  methods: {
    onMouseOver : function() {
      this.note.mouseover = true;
    },
    onMouseLeave : function() {
      this.note.mouseover = false;
    },
    onClickDelete : function(parentNote, note) {
      this.$emit('delete', parentNote, note);
    },
    onClickEdit : function(note) {
      this.$emit('editStart', note);
    },
    onEditEnd : function() {
      this.$emit('editEnd');
    },
    onClickChildNote : function(note) {
      this.$emit('addChild', note);
    },
    onClickAddNoteAfter : function(parentNote, note) {
      this.$emit('addNoteAfter', parentNote, note);
    },    
  },
  components: {
    draggable,
  },
}
</script>

<style scoped lang="scss">
.note {
  margin: 10px 0;
  display: flex;
  align-items: center;
  padding: 5px;
  color: rgba(25, 23, 17, 0.6);
  &.mouseover {
    background-color: rgb(232, 231, 228);
    cursor: pointer;
  }
  .note-icon {
    margin-left: 10px;
  }
  .note-name {
    width: 100%;
    padding: 3px 10px;
  }
  .buttons {
    display: flex;
    flex-direction: row;
    .button-icon {
      padding: 3px;
      margin-left: 3px;
      border-radius: 5px;
    }
  }
}
.child-note {
  padding-left: 10px;
}
</style>