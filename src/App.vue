<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance" />
    <BudgetList :list="sortedList()" @deleteItem="onDeleteItem" @showPositive="onlyPositive" @showNegative="onlyNegative" @showAll="showAll"/>
  </div>
</template>

<script>
import BudgetList from '@/components/BudgetList';
import TotalBalance from '@/components/TotalBalance';
import Form from '@/components/Form';

export default {
  name: 'app',
  components: {
    BudgetList,
    TotalBalance,
    Form,
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
      },
    },
    checker: 0
  }),
  computed: {
    totalBalance() {
      return Object.values(this.sortedList()).reduce((acc, item) => {
        return acc + item.value;
      }, 0) 
    },
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      }

      this.$set(this.list, newObj.id, newObj);
    },
    onlyPositive() {
      this.checker = 1;
    },
    onlyNegative() {
      this.checker = 2;
    },
    showAll() {
      this.checker = 0;
    },
    sortedList() {
      if (this.checker === 1) {
        return Object.values(this.list).filter(el => el.value > 0).reduce((acc, item) => {
          acc[item.id] = item;
          return acc;
        }, {});
      } else if (this.checker === 2) {
          return Object.values(this.list).filter(el => el.value < 0).reduce((acc, item) => {
            acc[item.id] = item;
            return acc;
          }, {});
      } else {
        return this.list;
      }
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
