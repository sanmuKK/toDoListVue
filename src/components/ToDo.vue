<template>
  <div class="tododiv">
    <div class="tag" @click="sendIndex">
      {{ msg }}
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDo",

  props: {
    msg: String,
    index: Number,
  },

  methods: {
    sendIndex() {
      this.$emit("getIndex", this.index, this.msg);
    },
  },
};
</script>

<style scoped>
.tododiv {
  height: 260px;
  width: 240px;
  float: left;
  margin-left: 52px;
  margin-top: 30px;
}

.tag {
  height: 240px;
  width: 240px;
  border: 2px solid orange;
  border-radius: 10px;
  background-color: orange;
  padding-left: 2px;
  word-wrap: break-word;
  word-break: normal;
  overflow-y: auto;
  text-align: justify;
  float: left;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 20px;
}

.close {
  float: right;
  position: relative;
  border-radius: 10px;
  background-color: transparent;
  border: 0px solid #3465a4;
  color: #ddd;
  visibility: visible;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
}
</style>
