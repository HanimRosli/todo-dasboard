<template>
<div>
    <div class="row justify-content-md-center">
        <div class="col-4 p-5">
            <div class="row justify-content-between align-items-center">
                <h3 class="mb-0">Todo List</h3>
                <b-button variant="success" @click="onClickAdd">Add</b-button>
            </div>
        </div>
    </div>
    <div class="row">
        <b-card v-for="(todo) in todos" :key="todo.id" :title="todo.title" class="col-12 mb-3">
            {{todos.description}}
        </b-card>
    </div>

    <b-modal id="modal-add-todo" title="Add Todo" @ok="handleOk">
        <b-form>
            <b-form-group label="Title:">
                <b-form-input v-model="form.title" placeholder="Add title"></b-form-input>
            </b-form-group>

            <b-form-group label="Decription">
                <b-form-textarea id="textarea" v-model="form.description" placeholder="Enter something..." rows="3" max-rows="6"></b-form-textarea>
            </b-form-group>
        </b-form>
    </b-modal>

</div>
</template>

<script>
export default {
    name: "Home",

    data() {
        return {
            todos: [],
            form: {
                title: '',
                description: ''
            }
        }
    },

    mounted() {
        this.getTodos()
    },

    methods: {
        getTodos() {
            this.$http.get('http://localhost:3000/todos')
                .then(res => {
                    this.todos = res.data
                })
        },

        onClickAdd() {
            this.$bvModal.show('modal-add-todo')
        },

        handleOk() {
            console.log('Ok')
        }
    },
};
</script>
