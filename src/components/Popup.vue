<template>
  <div v-if="isVisible" class="popup-overlay" @click="closePopup">
    <div class="popup" @click.stop>
      <h2>Заголовок</h2>
      <form @submit.prevent="submitForm">
        <div class="form">
          <!-- Динамическое создание полей для ввода -->
          <div
            class="input-group"
            v-for="(input, index) in inputs"
            :key="index"
          >
            <input
              type="text"
              v-model="input.value"
              :placeholder="input.placeholder"
            />
          </div>
        </div>
        <button type="submit">Отправить</button>
      </form>
    </div>
  </div>
   <!-- Отображение введенных данных после отправки формы -->
  <div v-if="submittedData" class="submitted-data">
    <h3>Введенные данные:</h3>
    <ul>
      <li v-for="(inputs, index) in submittedData" :key="index">
        {{ inputs.placeholder }}: {{ inputs.value }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isVisible: false, // Флаг видимости модального окна
      inputs: [
        { placeholder: "Имя", value: "" },
        { placeholder: "Email", value: "" },
        { placeholder: "Телефон", value: "" },
        { placeholder: "Адрес", value: "" },
        { placeholder: "Комментарий", value: "" },
      ],
      submittedData: null, // данные, введенные в форму
    }
  },
  methods: {
    openPopup() {
      this.isVisible = true // открытие модального окна
    },
    closePopup() {
      this.isVisible = false // Закрытие модального окна
    },
    submitForm() {
      this.submittedData = JSON.parse(JSON.stringify(this.inputs)) // Сохраняем данные
      this.inputs = this.inputs.map((input) => ({ ...input, value: "" })) // Очищаем поля
      this.closePopup()
    },
  },
}
</script>

<style scoped>
.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.popup {
  background-color: white;
  max-width: 500px;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.input-group {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.form {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

@media (max-width: 600px) {
  .input-group {
    flex-direction: column;
  }
}
</style>
