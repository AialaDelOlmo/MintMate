<template>
    <div>
        <button @click="showModal = true">Agregar movimiento</button>
        <teleport to="#app">
            <Modal v-show="showModal">
                <form @submit.prevent="submit">
                    <div class="field">
                        <label for="description">Título:</label>
                        <input type="text" v-model="title" required>
                    </div>
                    <div class="field">
                        <label for="amount">Cantidad:</label>
                        <input type="Number" id="amount" v-model="amount" required>
                    </div>
                    <div class="field">
                        <label for="description">Descripción:</label>
                        <textarea rows="4" v-model="description" required></textarea>
                    </div>
                    <div class="field">
                        <label>Tipo de movimiento</label>
                        <label class="radio-label">
                            <input type="radio" value="ingreso" v-model="movementType" />
                            <span>Ingreso</span>
                        </label>
                        <label class="radio-label">
                            <input type="radio" value="gasto" v-model="movementType" />
                            <span>Gasto</span>
                        </label>
                    </div>
                    <div class="action">
                        <button>Agregar movimiento</button>
                    </div>
                </form>
            </Modal>
        </teleport>
    </div>
</template>

<script setup>
    import { ref, defineEmits } from "vue";
    import Modal from "./Modal.vue";

    const showModal = ref(false);
    const title = ref("");
    const amount = ref(0);
    const description = ref("");
    const movementType = ref("ingreso");

    const emit = defineEmits(["create"]);
    const submit = () => {
      showModal.value = !showModal.value;
      emit("create", {
        title: title.value,
        description: description.value,
        amount: movementType.value === "ingreso" ? parseFloat(amount.value) : -parseFloat(amount.value),
        time: new Date(),
        id: new Date().getTime()
      });
      title.value = "";
      amount.value = 0;
      description.value = "";
      movementType.value = "ingreso";
      
    }
</script>   

<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}

.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: var(--brand-blue);
}

form {
  font-size: 1.24rem;
  width: 100%;
  background: #fff;
}
</style>