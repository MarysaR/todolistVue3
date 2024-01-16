<template>
  <div class="container">
    <h3 class="text-center mt-5">Une tâche à accomplir aujourd'hui ?</h3>

    <!-- INPUT -->
    <div class="d-flex">
      <input
        v-model="todo"
        type="text"
        placeholder="Ajoute une mission"
        class="form-control"
      />
      <button class="btn btn-warning rounded-1" @click="submitTodo">Start</button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr >
          <th scope="col">Mission</th>
          <th scope="col">Statut</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="index">
          <td>{{todo.name}}</td>
          <td>{{todo.status}}</td>
          <td>
            <div class="text-center" @click="editTodo(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="removeTodo(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todo: '',
      editTodoData: null,
      todos: [
        {
          name: "Promener le chat",
          status: "A faire",
        },
        {
          name: "Nourrir les plantes carnivores",
          status: "En cours",
        },
        {
          name: "Créer une to do list",
          status: "Terminée",
        }
      ]
    }
  },

      methods : {
      submitTodo() {
        // console.log(this.todo)
        if (this.todo.lenght === 0) return;
        
        if (this.editTodoData === null) {
          this.todos.push({
            name: this.todo,
            status: 'A faire'
          });
      } else {
        this.todos[this.editTodoData].name = this.todo;
        this.editTodoData = null;
      }

        this.todo = '';
      },

      editTodo(index) {
        this.todo = this.todos[index].name;
        this.editTodoData = index;
      },

      removeTodo(index) {
       this.todos.splice(index, 1);
      }
    }
  };
</script>

<!-- <style>
</style> -->
