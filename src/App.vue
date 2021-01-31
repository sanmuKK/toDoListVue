<template>
  <div id="app">
    <Add @todo="addNew"></Add>
    <ToDo
      v-for="(toDo, i) in toDos"
      :msg="toDo.msg"
      :index="i"
      :key="toDo.id"
      @getIndex="showModal"
    ></ToDo>
    <Edit
      :show="show"
      :title="title"
      :toDo="toDoConnnent"
      :index="editIndex"
      @hideModal="hideModal"
      @delToDo="deleteToDo"
      @editToDo="editToDo"
    ></Edit>
  </div>
</template>

<script>
import ToDo from "./components/ToDo.vue";
import Add from "./components/Add.vue";
import Edit from "./components/Edit.vue";

export default {
  name: "App",

  components: {
    Add,
    ToDo,
    Edit,
  },

  data() {
    return {
      toDos: [{ id: 0, msg: "单击便签编辑ToDo" }],
      id: 1,
      title: "编辑ToDo",
      show: false,
      editIndex: 0,
      toDoConnnent: "",
    };
  },

  created: function () {
    if (!localStorage.getItem("todolists"))
      localStorage.setItem("todolists", JSON.stringify(this.toDos));
    this.toDos = JSON.parse(localStorage.getItem("todolists"));
  },

  methods: {
    addNew: function (data) {
      if (data) {
        this.toDos.push({
          id: this.id,
          msg: data,
        });
        localStorage.setItem("todolists", JSON.stringify(this.toDos));
      } else alert("ToDo不可为空");
    },

    deleteToDo: function (data) {
      localStorage.setItem("todolists", JSON.stringify(this.toDos));
      this.toDos.splice(data, 1);
      this.show = false;
    },

    showModal(data1, data2) {
      this.toDoConnnent = data2;
      this.ifFocus = true;
      this.editIndex = data1;
      this.show = true;
    },

    editToDo: function (data) {
      if (data) {
        this.toDos[this.editIndex].msg = data;
        localStorage.setItem("todolists", JSON.stringify(this.toDos));
        this.show = false;
      } else alert("ToDo不可为空");
    },

    hideModal() {
      this.show = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  background: url(./assets/123.jpg) no-repeat fixed;
  background-size: cover;
}
::-webkit-scrollbar {
  width: 6px;
  height: 6px;
  background-color: black;
}

::-webkit-scrollbar-track {
  border-radius: 10px;
  background-color: rgba(240, 240, 240, 0.5);
}

::-webkit-scrollbar-thumb {
  border-radius: 10px;
  box-shadow: inset 0 0 0px rgba(240, 240, 240, 0.5);
  background-color: rgba(240, 240, 240, 0.5);
}
</style>
