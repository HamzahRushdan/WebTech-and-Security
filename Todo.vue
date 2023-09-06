<script>
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
        ]
    }),

    watch: {
    },

    mounted() {
    },

    computed: {
    },

    // methods that implement data logic
    methods: {
    }
}
</script>

<template>
    <section class="todoapp">
        <header class="header">
            <h1>Todos</h1>
            <input autofocus class="new-todo" type="text" placeholder="What needs to be done?">
        </header>
        <section class="main">
            <input class="toggle-all" id="toggle-all" type="checkbox" checked="false">
            <label for="toggle-all">Mark all as complete</label>
            <ul class="todo-list">
                <li class="todo-item">
                    <!-- NOTE - change to view-todo -->
                    <div class="view"> 
                        <!-- NOTE - change to toggle-done -->
                        <input class="toggle" type="checkbox">
                        <label>{{ todos[0].title }}</label>
                        <!-- NOTE: Change to remove-todo -->
                        <button class="destroy"></button>
                    </div>
                    <!-- NOTE: Change to edit-todo -->
                    <!-- <input class="edit" type="text" placeholder="Exiting todo to edit"> -->
                </li>
            </ul>
        </section>
        <footer class="footer">
            <span class="todo-count">
                <strong>1</strong>
                <span>item left</span>
            </span>
            <ul class="filters">
                <li>
                    <a href="#/all">All</a>
                </li>
                <li>
                    <a href="#/active">Active</a>
                </li>
                <li>
                    <a href="#/completed">Completed</a>
                </li>
            </ul>
            <button class="clear-completed">
                Clear completed todos
            </button>
        </footer>
    </section>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
