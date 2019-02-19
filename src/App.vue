<template>
  <div id="app">
    <h1>amp-test</h1>
    <amplify-connect :query="listTodosQuery">
      <template slot-scope="{loading, data, errors}">
        <div v-if="loading">Loading...</div>

        <div v-else-if="errors.length > 0"></div>

        <div v-else-if="data">
          <TodoList :items="data.listTodos.items"></TodoList>
        </div>
      </template>
    </amplify-connect>
  </div>
</template>

<script>
import { components } from 'aws-amplify-vue'
import TodoList from '@/components/TodoList.vue';
const ListTodosQuery = `query ListTodos {
    listTodos {
      items {
        id
        name
      }
    }
  }`;

export default {
  name: 'app',
  components: {
    TodoList,
    ...components
  },
  computed: {
    listTodosQuery() {
      return this.$Amplify.graphqlOperation(ListTodosQuery);
    }
  }
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
