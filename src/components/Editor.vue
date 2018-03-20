<template>
  <div id="note-editor">
    <div class="form-group">
      <input type="text" name="title"
             class="title form-control"
             placeholder="请输入标题"
             @input="updateNote"
             v-model="currentNote.title">
      <textarea
        v-model="currentNote.content" name="content"
        class="form-control" row="3" placeholder="请输入正文"
        @input="updateNote"></textarea>
    </div>
  </div>
</template>

<script>
  import { editNote } from '../vuex/actions'

  export default {
    computed: {
      // 通过计算属性得到的一个对象，这样子我们就能愉快的使用 v-model 了
      currentNote () {
        return this.$store.getters.activeNote;
      }
    },
    methods: {
      // 因为在严格模式中不允许直接在模板层面去修改 state 中的值
      updateNote() {
        editNote(this.$store,this.currentNote);
      }
    }
  }
</script>

<style scoped>
  #note-editor {
    float: left;
    width : calc(100% - 130px);
  }
</style>