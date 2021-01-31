<template>
  <div class="center">
    <input
      id="todo"
      class="input1"
      type="text"
      placeholder="添加ToDo"
      v-model="connent"
    />
    <button id="btn" class="sub" @click="add">提交</button>
  </div>
</template>
<script>
export default {
  name: "Add",
  data() {
    return {
      connent: "",
    };
  },
  methods: {
    add() {
      this.$emit("todo", this.connent);
      this.connent = "";
    },
  },
};
</script>
<style scoped>
.sub {
  cursor: pointer;
  margin-left: 5px;
}

.input1 {
  border-radius: 4px;
  width: 300px;
  height: 20px;
}

.center {
  text-align: center;
  margin-top: 20px;
  margin-bottom: 30px;
}
</style>
