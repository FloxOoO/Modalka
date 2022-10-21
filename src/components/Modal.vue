<template>
  <div v-if="isOpen" class="backdrop" @click="close">
    <div class="modal" @click.stop>
      <h1>Уведомление</h1>
      <hr />
      <slot></slot>
      <hr />
      <div class="footer">
        <slot name="actions" :close="close" :confirm="confirm">
          <button @click="close">Отмена</button>
          &nbsp;
          <button @click="confirm">OK</button>
        </slot>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  currentModalController: null,
  data() {
    return {
      isOpen: false,
    };
  },
  mounted() {
    document.addEventListener("keydown", this.handleKeydown);
  },
  beforeUnmount() {
    document.removeEventListener("keydown", this.handleKeydown);
  },
  methods: {
    handleKeydown(e) {
      if (this.isOpen && e.key === "Escape") {
        this.close();
      }
    },
    open() {
      let resolve;
      let reject;
      const modalPromise = new Promise((ok, fail) => {
        resolve = ok;
        reject = fail;
      });
      this.$options.currentModalController = { resolve, reject };
      this.isOpen = true;
      return modalPromise;
    },
    close() {
      this.$options.currentModalController.resolve(false);
      console.log(this.$options.currentModalController);
      this.isOpen = false;
    },
    confirm() {
      this.$options.currentModalController.resolve(true);
      this.isOpen = false;
    },
  },
};
</script>
<style>
.modal {
  top: 50px;
  padding: 20px;
  left: 50%;
  transform: translateX(-50%);
  position: fixed;
  z-index: 101;
  background-color: white;
  border-radius: 10px;
}
.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 100;
}
.footer {
  text-align: rigth;
}
.modal h1 {
  text-align: center;
  margin: 0;
}
</style>
