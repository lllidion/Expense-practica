<template>
  <div id="app">
    <h1>Трекер Расходов</h1>
    <input v-model="description" placeholder="Описание">
    <input v-model.number="amount" type="number" placeholder="Сумма">
    <button @click="addNewExpense">Добавить Расход</button>
    <ul>
      <li v-for="expense in expenses" :key="expense.id">
        {{ expense.description }} - {{ expense.amount }} руб.
      </li>
    </ul>
    <h2>Итого: {{ totalExpenses }} руб.</h2>
  </div>
</template>

<script>
import { mapState, mapActions, mapGetters } from 'vuex';

export default {
  data() {
    return {
      description: '',
      amount: 0
    };
  },
  computed: {
    ...mapState(['expenses']),
    ...mapGetters(['totalExpenses'])
  },
  methods: {
    ...mapActions({
      addExpenseAction: 'addExpense' // Переименование для избежания конфликта
    }),
    addNewExpense() {
      if (this.description.trim() && this.amount > 0) {
        this.addExpenseAction({
          id: Date.now(),
          description: this.description,
          amount: parseFloat(this.amount)
        });
        this.description = '';
        this.amount = 0;
      } else {
        alert("Пожалуйста, заполните все поля и убедитесь, что сумма больше нуля.");
      }
    }
  }
};
</script>

<style>
body {
  font-family: 'Arial', sans-serif;
  background-color: #f8f8f8;
  color: #333;
  margin: 0;
  padding: 20px;
}

#app {
  max-width: 600px;
  margin: auto;
  background: white;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

h1 {
  color: #5c007a;
}

input, button {
  padding: 10px;
  margin: 5px 0;
  border: 2px solid #ccc;
  border-radius: 4px;
  display: block;
  width: 100%;
}

button {
  background-color: #5c007a;
  color: white;
  cursor: pointer;
  border: none;
}

button:hover {
  background-color: #7a009e;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

li:last-child {
  border-bottom: none;
}

h2 {
  color: #333;
  border-top: 1px solid #ccc;
  padding-top: 10px;
}
</style>
