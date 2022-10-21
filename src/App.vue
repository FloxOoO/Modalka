<template>
  <button @click="openModal">Открыть</button>
  <Modal ref="confirmationModal">
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
    return { confirmation: "" };
  },
  methods: {
    async openModal() {
      this.confirmation = "";
      const modalResult = await this.$refs.confirmationModal.open();
      if (modalResult) {
        alert("Confirmed");
      }
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
