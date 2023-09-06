<script>

const filters = {
    all: (todos) => todos,
    active: (todos) => todos.filter((todo) => !todo.completed),
    completed: (todos) => todos.filter((todo) => todo.completed)
};

export default {
    name: 'TodoApp',
    
    // app initial state
    data: () => ({
        todos: [
            {
                id: Date.now(),
                title: 'Todo Item',
                completed: false,
            }
        ],
        visibility: 'all',
        beforeEditCancel: null,
        editedTodo: null
    }),

    watch: {
    },

    mounted() {
        window.addEventListener('hashchange', this.onHashChange)
        this.onHashChange()
    },

    computed: {
        remaining() {
            return this.todos.length;
        },
        filteredTodos() {
            return filters[this.visibility](this.todos);
        }
    },

    // methods that implement data logic
    methods: {
        onHashChange() {
            var visibility = window.location.hash.replace(/#\/?/, '');
            if (filters[visibility]) {
                this.visibility = visibility;
            } else {
                window.location.hash = '';
                this.visibility = 'all';
            }
        },
        toggleAll(e) {
            this.todos.forEach((todo) => (todo.completed = e.target.checked))
        },
        removeCompleted() {
            this.todos = filters.active(this.todos)
        },
        addTodo(event) {
            // TODO: Add code here.
            const value = event.target.value.trim();

            if (!value) {
                return;
            }

            this.todos.push({
                id: Date.now(),
                title: value,
                isCompleted: false
            });

            event.target.value = ''
        },
        removeTodo(todo) {
            this.todos.splice(this.todos.indexOf(todo), 1);
        },
        editTodo(todo) {
            this.beforeEditCancel = todo.title;
            this.editedTodo = todo;
        }
    }
}
</script>

<template>
    <section class="todoapp">
        <header class="header">
            <h1>Todos</h1>
            <input autofocus class="new-todo" placeholder="What needs to be done?" @keyup.enter="addTodo">
        </header>
        <section class="main" v-show="todos.length">
            <input class="toggle-all" id="toggle-all" type="checkbox" :checked="remaining === 0" @change="toggleAll">
            <label for="toggle-all">Mark all as complete</label>
            <ul class="todo-list">
                <li v-for="todo in filteredTodos" :key="todo.id" class="todo-item" :class="{ completed: todo.completed, editing: todo === editedTodo }">
                    <!-- NOTE - change to view-todo -->
                    <div class="view"> 
                        <!-- NOTE - change to toggle-done -->
                        <input class="toggle" type="checkbox" v-model="todo.completed">
                        <label @dblclick="editTodo(todo)">{{ todo.title }}</label>
                        <!-- NOTE: Change to remove-todo -->
                        <button class="destroy" @click="removeTodo(todo)"></button>
                    </div>
                    <!-- NOTE: Change to edit-todo -->
                    <input
                        v-if="todo === editedTodo"
                        class="edit"
                        type="text"
                        v-model="todo.title"
                        @vnode-mounted="({ el }) => el.focus()"
                    >
                </li>
            </ul>
        </section>
        <footer class="footer" v-show="todos.length">
            <span class="todo-count">
                <strong>{{ remaining }}</strong>
                <span>{{ remaining === 1 ? ' item' : ' items' }} left</span>
            </span>
            <ul class="filters">
                <li>
                    <a href="#/all" :class="{ selected: visibility === 'all' }">All</a>
                </li>
                <li>
                    <a href="#/active" :class="{ selected: visibility === 'active' }">Active</a>
                </li>
                <li>
                    <a href="#/completed" :class="{ selected: visibility === 'completed' }">Completed</a>
                </li>
            </ul>
            <button class="clear-completed" @click="removeCompleted" v-show="todos.length > remaining">
                Clear completed todos
            </button>
        </footer>
    </section>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
