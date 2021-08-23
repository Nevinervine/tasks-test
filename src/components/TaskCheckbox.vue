<template>
  <div  class="tasks-editor__item">
    <input type="text" placeholder="Название вопроса"  v-model="data.title" class="tasks-editor__item-header"/>
    <div v-for="(question,j) in data.questions" :key="keys+''+j">
      <div class="tasks-editor__item-input">
        <input v-model="question.checked" :name="name" type="checkbox">
        <input v-model="question.description" type="text">
      </div>
    </div>
    <div @click="addNewInp(data)" class="tasks-editor__item-add">Добавить</div>
  </div>
</template>

<script>
export default {
  name: "TaskRadio",
  props: {
    name:String,
    data:String | Number | Boolean | Object,
    keys:String | Number | Boolean | Object,
  },
  data() {
    return {
      value:this.data.description,
      oldValue:this.data.description
    }
  },
  methods: {
    addNewInp(inp){
      inp.questions.push({checked:false,description:'название'});
      this.textСhanged=true;
    },
  }
}
</script>


<style lang="scss" scoped>

.tasks-editor {
  &__item {
    border: 1px solid #000000;
    padding: 10px;
    margin-bottom: 10px;

    &-header {
      margin-bottom: 7px;
      border: 1px solid #000000;
    }
    &-input {
      margin-bottom: 8px;
    }
    &-add {
      color: #000000;
      cursor: pointer;
    }
  }
}
</style>
