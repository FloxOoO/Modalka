<template>
  <button @click="isOpen = true">Открыть</button>
  <Modal :is-open="isOpen" @close="isOpen = false" @ok="modalOK">
    Учишь слоты?
    <template #actions="{ confirm }">
      <input :placeholder="$options.MODAL_TEXT" v-model="confirmation" />
      <button :disabled="!confirmed" @click="confirm">OK</button>
    </template>
  </Modal>
</template>

<script>
import Modal from "./components/Modal.vue";
export default {
  name: "App",
  components: {
    Modal,
  },
  MODAL_TEXT: "ПОДТВЕРЖДАЮ",
  data() {
    return { isOpen: false, confirmation: "" };
  },
  methods: {
    modalOK() {
      alert("Вы правы!!!");
    },
  },
  computed: {
    confirmed() {
      return this.confirmation === this.$options.MODAL_TEXT;
    },
  },
};
</script>

<style>
</style>
