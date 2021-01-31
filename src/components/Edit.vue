<template>
  <div class="modal-bg" v-show="show">
    <div class="modal-container">
      <div class="modal-header">
        {{ title }}
      </div>
      <textarea class="modal-text" v-model="toDo" v-focus></textarea>
      <div class="modal-footer">
        <button class="modal-btn" @click="hideModal">取消</button>
        <button class="modal-btn" @click="delToDo">删除</button>
        <button class="modal-btn" @click="editToDo">确认</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "modal",
  props: {
    show: {
      type: Boolean,
      default: false,
    },

    title: {
      type: String,
      default: "",
    },

    toDo: {
      type: String,
      default: "",
    },

    index: {
      type: Number,
      default: 0,
    },
  },

  data() {
    return {
      x: 0,
      y: 0,
      node: null,
      isCanMove: false,
    };
  },

  directives: {
    focus: function (e) {
      e.focus();
    },
  },

  mounted() {
    this.node = document.querySelector(".modal-container");
  },
  methods: {
    hideModal() {
      this.$emit("hideModal");
    },

    delToDo() {
      this.$emit("delToDo", this.index);
    },

    editToDo() {
      this.$emit("editToDo", this.toDo);
    },

    setStartingPoint(e) {
      this.x = e.clientX - this.node.offsetLeft;
      this.y = e.clientY - this.node.offsetTop;
      this.isCanMove = true;
    },

    modalMove(e) {
      if (this.isCanMove) {
        this.node.style.left = e.clientX - this.x + "px";
        this.node.style.top = e.clientY - this.y + "px";
      }
    },

    cancelMove() {
      this.isCanMove = false;
    },
  },
};
</script>

<style scoped>
.modal-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 10;
}
.modal-container {
  background: #fff;
  border-radius: 10px;
  overflow: hidden;
  position: fixed;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 40%;
  height: 40%;
}
.modal-header {
  height: 56px;
  background: #409eff;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: move;
}
.modal-footer {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 57px;
  border-top: 1px solid #ddd;
}
.modal-footer button {
  width: 100px;
  height: 30px;
  margin-left: 10px;
  margin-right: 10px;
  border-radius: 6px;
}
.modal-text {
  height: 180px;
  width: 430px;
  resize: none;
  border-radius: 5px;
  background-color: rgba(241, 241, 241, 0.98);
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 16px;
  margin-top: 4px;
}
</style>