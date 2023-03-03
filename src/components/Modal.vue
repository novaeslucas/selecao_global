<template>
  <div v-if="show" class="modal">
    <div class="modal-overlay" @click="fechar"></div>
    <div class="modal-container">
      <div class="modal-header">
        <h3>{{ titulo }}</h3>
        <button @click="fechar">&times;</button>
      </div>
      <div class="modal-body">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      required: true,
    },
    titulo: {
      type: String,
      required: true,
    },
  },
  methods: {
    fechar() {
      this.$emit("fechar");
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1000;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-container {
  position: relative;
  background-color: #fff;
  border-radius: 4px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  max-width: 90%;
  max-height: 90%;
  overflow: auto;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}

.modal-body {
  padding: 10px;
}
</style>
