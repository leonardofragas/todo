<template>
    <div id="todo-list">
        <div id="new-todo-list-item">
            <input type="text" placeholder="digite sua tarefa :)" id="new-todo-list-item-input" @keyup="updateItemText" />
            <input type="submit" id="new-todo-list-item-submit" @click="newItem" value="adicionar" />
        </div>
        <div class="list-item" v-for="n in todos" :key="n.id">
            <div class="list-item-holder" v-if="n.location == location" :data-status="n.completed">
                <div class="checkbox-items" :data-status="n.completed">
                    <input type="checkbox" :data-id="n.id" :id="n.id" @click="updateTodo" :checked="n.completed" /> <label :data-id="n.id" :for="n.id" >{{ n.name }}</label>
                </div>
                <div class="item-options">
                    <div class="delete-item" @click="deleteItem" :data-id="n.id">Apagar</div>
                    <div class="archive-item" v-if="n.location !== 'archive'" @click="archiveItem" :data-id="n.id">Arquivar</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { useStore } from 'vuex'
import { v4 as uuidv4 } from 'uuid'

export default {
    name: 'TodoList',
    data() {
        return {
            newTodoItem: ''
        }
    },

    props: {
        location: String
    },

    setup() {
        const store = useStore()
        return {
            todos: store.getters.todos
        }
    },

    methods: {
        updateTodo: function(e) {
            let newStatus = e.currentTarget.parentElement.getAttribute('data-status') == "true"? false : true

            this.$store.commit('updateTodo', {
                id: e.currentTarget.getAttribute('data-id'),
                completed: newStatus
            })
        },

        updateItemText: function(e) {
            this.newTodoItem = e.currentTarget.value
            if (e.keyCode === 13) {
                this.newItem()
            }

            return false
        },

        deleteItem: function(e) {
            this.$store.commit('deleteTodo', {
                id: e.currentTarget.getAttribute('data-id')
            })
        },

        newItem: function () {
            if(this.newTodoItem !== '') {
                this.$store.commit('addTodo', {
                    id: uuidv4(),
                    name: this.newTodoItem,
                    completed: false
                })
            }

            // e.currentTarget.getAttribute('value') = ''
            this.newTodoItem = ''
        },

        archiveItem: function(e) {
            this.$store.commit('moveTodoItem', {
                id: e.currentTarget.getAttribute('data-id'),
                location: 'archive'
            })
        }
    }
}
</script>

<style scoped>
#todo-list {
    width: 100%;
    margin: 0 auto;
    border-radius: 14px;
    /* max-width: 400px; */
    border: 2px solid #ddd;
}
.list-item-holder {
    display: flex;
    padding: 1rem 1rem;
    justify-content: space-between;
    border-bottom: 1px solid #ddd;
}
.item-options, .item-checkbox  {
    display: flex;
}
#new-todo-list-item {
    display: flex;
    justify-content: center;
    align-content: flex-end;
    padding: 1rem;
}
.delete-item, .archive-item {
    font-size: 0.875rem;
    background: rgb(220, 220, 220);
    margin: 0 0 0 0.5rem;
    height: 1rem;
    border-radius: 100px;
    transition: all 0.1s ease-out;
    color: rgba(0,0,0,0.5);
    cursor: pointer;
    padding: 0.25rem 0.75rem;
}
.checkbox-items {
    display: flex;
    align-items: center;
}
.delete-item:hover, .archive-item:hover {
    background: #ddd;
    color: black;
    transform: scale(0.90);
}
[data-status="false"] label {
    color: #3d3f49;
    font-weight: 600;
}
[data-status="true"] label {
    color: rgb(211, 23, 83);
    text-decoration: line-through;
}
</style>