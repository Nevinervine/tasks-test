<template>
  <div class="tasks-editor">
    <div class="tasks-editor__header">
      <div class="tasks-editor__part tasks-editor__part--left">
        <div @click="returnDate" class="tasks-editor__arrow">
          <-
        </div>
        <div class="tasks-editor__title">{{ title.name }}</div>
      </div>
      <div class="tasks-editor__part tasks-editor__part--right">
        <div @click="save" :class="{ 'tasks-editor__save--disabled' : textСhanged == false}" class="tasks-editor__save">
          Сохранить
        </div>
      </div>
    </div>
    <div class="tasks-editor__add">
      <div @click="addCheckbox" ref="child" class="tasks-editor__add-item">
        <input type="checkbox" id="tasks-checkbox">
        <div class="tasks-editor__add-checkbox-">Добавить</div>
      </div>
      <div @click="addRadio" ref="child" class="tasks-editor__add-item">
        <input type="radio" id="tasks-radio">
        <div class="tasks-editor__add-radio">Добавить</div>
      </div>
    </div>


    <div v-if="">
      <div v-for="(item,i) in tasks" :key="i" class="tasks-editor__container">
        <div :is="item.type" :data="item" :keys="i"></div>
      </div>
    </div>


  </div>
</template>
<script>
import TaskRadio from './components/TaskRadio.vue'
import TaskCheckbox from './components/TaskCheckbox.vue'

export default {
  name: "TasksEditor",
  components: {
    TaskRadio,
    TaskCheckbox
  },
  props: {
    dataTask: String | Number | Boolean | Object,
    title: String | Number | Boolean | Object,
  },
  data() {
    return {
      textСhanged: false,
      tasks: this.dataTask,
      oldTasks: JSON.parse(JSON.stringify(this.dataTask)),
    }
  },
  methods: {
    addCheckbox() {
      this.tasks.push({
        type: "TaskCheckbox",
        title: "",
        questions: [{checked: false, description: ''}, {checked: false, description: ''}]
      });
      this.textСhanged = true;
    },
    addRadio() {
      this.tasks.push({
        type: "TaskRadio",
        title: "",
        questions: [{checked: false, description: ''}, {checked: false, description: ''}]
      });
      this.textСhanged = true;
    },
    save() {
      if (this.textСhanged) {
        this.$emit("saveData");
        this.oldTasks = JSON.parse(JSON.stringify(this.tasks));
        this.textСhanged = false;
      }
    },
    returnDate() {
      this.$emit("retunDate");
    }
  },
  watch: {
    tasks: {
      handler: function (newValue) {
        if (JSON.stringify(this.oldTasks) === JSON.stringify(this.tasks)) {
          this.textСhanged = false;
        } else {
          this.textСhanged = true;
        }
      },
      deep: true
    }
  }
}


</script>
<style lang="scss" scoped>
.tasks-editor {
  padding: 20px;
  max-width: 300px;
  &__arrow{
    margin-right: 20px;
    cursor: pointer;
  }
  &__header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
  }
  &__save {
    background: #C4C4C4;
    padding: 5px 17px;
    cursor: pointer;

    &--disabled {
      cursor: not-allowed;
      background-color: rgb(229, 229, 229) !important;
      color: gray;
      pointer-events: none;
    }
  }
  &__part {
    display: flex;
  }
  &__add {
    display: flex;
    margin-bottom: 20px;

    &-item {
      border: 1px solid #000000;
      margin-right: 15px;
      padding: 5px;
      display: flex;
      cursor: pointer;
    }
  }
}
</style>
