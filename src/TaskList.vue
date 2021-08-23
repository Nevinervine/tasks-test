<template>
  <div>
    <div @click="newEdit()">Новый вопрос</div>
    <div v-for="(data,i) in dataTasks">
      <div v-if="show==false" @click="showEdit(i)">{{ data.name }}</div>
    </div>
    <tasks-editor @retunDate="returData" @saveData="save" v-if="show==true" :title="currTask" :dataTask="currTask.question"/>
  </div>
</template>

<script>
import TasksEditor from './TasksEditor.vue'

export default {
  name: "TaskList",
  components: {
    TasksEditor
  },
  mounted() {
    if(localStorage.task){
      this.dataTasks =  JSON.parse (localStorage.task);
      this.oldDataTasks= JSON.parse (localStorage.task);
    }
  },
  data() {
    return {
      oldDataTasks: [],
      dataTasks:[],
      show: false,
      currTask: undefined,
    }
  },
  methods: {
    showEdit(n) {
      this.show = true;
      this.currTask = this.dataTasks[n];
    },
    newEdit() {
      this.dataTasks.push({name: 'test' + parseInt(this.dataTasks.length + 1) + '', question: []});
      this.currTask = this.dataTasks[this.dataTasks.length - 1];
      this.show = true;
    },
    save(){
      this.oldDataTasks=this.dataTasks;
      localStorage.task = JSON.stringify(this.dataTasks);
    },
    returData(){
      this.show=false;
      this.dataTasks=this.oldDataTasks;
    }
  }
}
</script>

<style scoped>

</style>
