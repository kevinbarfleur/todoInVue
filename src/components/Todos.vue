<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos in Vue</h1>
      <div class="input-section">
        <input
          type="text"
          class="new-todo"
          placeholder="Ajouter une tache"
          v-model="newTodo"
          @keyup.enter="addTodo"
        />
      </div>
    </header>
    <div class="main">
      <ul class="todo-list">
        <!-- Affichage des todos: Pour chaque elements dans filteredTodo, on affiche -->
        <li class="todo" v-for="todo in filteredTodos" :key="todo.id">
          <input type="checkbox" v-model="todo.completed" />
          <!-- {completed: todo.completed} permet de changer dynamiquement la classe 
          à "completed" si dans le state, todo.completed = true"-->
          <label :class="{completed: todo.completed}">{{ todo.name }}</label>
          <div class="deleteButton" @click="deleteTodo(todo)">
            <i class="fas fa-trash"></i>
          </div>
        </li>
      </ul>
    </div>
    <footer class="footer">
      <span class="todo-count">
        <strong>{{ remaining }}</strong> Tâches à faire
      </span>
      <ul class="filters">
        <!-- Pareil qu'avec completed plus haut, la classe des lien 
        change en fonction de celle définie dans le state-->
        <li>
          <a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a>
        </li>
        <li>
          <a
            href="#"
            :class="{selected: filter === 'todo'}"
            @click.prevent="filter = 'todo'"
          >A faire</a>
        </li>
        <li>
          <a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a>
        </li>
      </ul>
    </footer>
  </section>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        {
          name: 'Tache de test',
          completed: false
        }
      ],
      newTodo: '',
      filter: 'all'
    }
  },
  methods: {
    addTodo() {
      // Ajout d'une nouvelle todo avec l'état non complété et le texte contenu dans l'input grace au v-model
      this.todos.push({
        completed: false,
        name: this.newTodo
      })
      // On vide l'input avec l'ajout de la todo
      this.newTodo = ''
    },
    deleteTodo(todo) {
      // Ici, grace à la fonction filter, on garde dans this.todo toute les todo sauf la todo en parametre
      this.todos = this.todos.filter(i => i !== todo)
    }
  },
  computed: {
    remaining() {
      return this.todos.filter(todo => !todo.completed).length
    },
    filteredTodos() {
      if (this.filter === 'todo') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === 'done') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    }
  }
}
</script>

<style lang="scss">
.todoapp {
  width: 70%;
  text-align: center;
  margin: 20% auto;

  input.new-todo {
    margin: 10% auto;
    padding: 2px 10px;
    width: 100%;
  }

  .main {
    text-align: left;

    .todo-list {
      margin: none;
    }
    .todo {
      list-style: none;

      &:hover {
        .deleteButton {
          opacity: 1;
          transition: 0.2s;
        }
      }

      input {
        margin: auto 2%;
      }
      label {
        margin: auto 2%;

        &.completed {
          opacity: 0.4;
          text-decoration: line-through;
        }
      }
      .deleteButton {
        cursor: pointer;
        opacity: 0;
        transition: 0.2s;
        float: right;
        color: #ff6e40;

        &:hover {
          transform: scale(1.2);
        }
      }
    }
  }

  .footer {
    margin: 20% auto;

    .filters {
      list-style: none;
      margin: 4% auto;

      li {
        display: inline;
        margin: auto 10px;

        a {
          text-decoration: none;
          color: #212121;
          margin: 5px auto;
          padding: 2px 5px;
          opacity: 0.4;

          &.selected {
            opacity: 1;
            border: 1px solid lightgray;
          }
        }
      }
    }
  }
}
</style>