<template>
    <div class="container">
        <div class="row">
            <div class="col-md-7">
                <form>
                    <div class="form-group row">
                        <label for="inputPassword" class="col-sm-2 col-form-label">Todo</label>
                        <div class="col-sm-10">
                            <input v-model="todoForm.task" type="text" class="form-control" id="inputPassword">
                        </div>
                    </div>
                    <div class="form-group row">
                        <label for="inputPassword" class="col-sm-2 col-form-label">Description</label>
                        <div class="col-sm-10">
                            <input v-model="todoForm.description" type="text" class="form-control" id="inputPassword">
                        </div>
                    </div>
                    <div class="form-group row">
                        <label for="inputPassword" class="col-sm-2 col-form-label">Time</label>
                        <div class="col-sm-10">
                            <input v-model="todoForm.time" type="text" class="form-control" id="inputPassword">
                        </div>
                    </div>
                    <button v-if="editStatus" @click.prevent="updateTodo" type="submit" class="btn btn-primary">Update</button>
                    <button v-else @click.prevent="addTodo" type="submit" class="btn btn-primary">Add</button>
                </form>
            </div>
        </div>
        <div class="row my-4">
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header text-center">
                        <button @click = "showTodo" class="btn btn-secondary">Task Todo</button>
                        <button @click = "showDoing" class="btn btn-primary">Task in Progress</button>
                        <button @click = "showDone" class="btn btn-success">Task Done</button>
                    </div>

                    <div class="card-body" id="ToDo">
                        <ul v-for="(todo, index) in tasks" :key="index">
                            <li v-if="todo.status == 'todo'">
                                <b>Todo:</b> {{todo.task}}
                                <p>
                                    <b>Description:</b> {{todo.description}} <br />
                                    <small>
                                       <b>Time:</b> {{todo.time}} 
                                       <br />
                                       <span class="mr-2">
                                           <a @click="editTodo(index)" >Edit</a> 
                                       </span>
                                       <span >
                                          <a @click="moveToDoing(index)" class="text-success mr-2">Update</a> 
                                       </span>
                                       <span >
                                          <a @click="cancelTodo(index)" class="text-danger">Cancel</a> 
                                       </span>
                                    </small>
                                </p>
                            </li>
                        </ul>
                    </div>

                    <div class="card-body bg-primary hide" id="Doing">
                        <ul v-for="(todo, index) in tasks" :key="index">
                            <li v-if="todo.status == 'doing'">
                                <b>Todo:</b> {{todo.task}}
                                <p>
                                    <b>Description:</b> {{todo.description}} <br />
                                    <small>
                                       <b>Time:</b> {{todo.time}}
                                       <br />
                                       <span class="mr-3" >
                                           <a @click="moveTodo(index)" class="text-white">Todo</a> 
                                       </span>
                                       <span >
                                          <a @click="moveToDone(index)" class="text-white">Done</a> 
                                       </span>
                                    </small>
                                </p>
                            </li>
                        </ul>
                    </div>

                    <div class="card-body bg-success hide" id="Done">
                        <ul v-for="(todo, index) in tasks" :key="index">
                            <li v-if="todo.status == 'done'">
                                <b>Todo:</b> {{todo.task}}
                                <p>
                                    <b>Description:</b> {{todo.description}} <br />
                                    <small>
                                       <b>Time:</b> {{todo.time}}
                                       <br />
                                       <span class="mr-3" >
                                           <a @click="moveToDoing(index)" class="text-white">Doing</a> 
                                       </span>
                                       <span >
                                          <a @click="cancelTodo(index)" class="text-danger">Delete</a> 
                                       </span>
                                    </small>
                                </p>
                            </li>
                        </ul>
                    </div>
                </div>
               
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                editStatus: false,
                index: null,
                todoForm: {
                    task: null,
                    description:  null,
                    time: null,
                    status: 'todo'
                },
                tasks: [
                    {
                        task: 'Shopping',
                        description: 'Buy valentine gift',
                        time: '2pm',
                        status: 'todo'
                    },
                    {
                        task: 'Assignment',
                        description: 'Complete assignment',
                        time: '12am',
                        status: 'doing'
                    },
                    {
                        task: 'Chill',
                        description: 'Hangout with girlfriends',
                        time: '4pm',
                        status: 'done'
                    }
                ]
            }
        },
        methods: {
            showTodo(){
                let ToDo = document.querySelector('#ToDo')
                let Doing = document.querySelector('#Doing')
                let Done = document.querySelector('#Done')
                ToDo.classList.remove('hide')
                ToDo.classList.add('show')
                Doing.classList.add('hide');
                Done.classList.add('hide');
                
            },
            showDoing(){
                let ToDo = document.querySelector('#ToDo')
                let Doing = document.querySelector('#Doing')
                let Done = document.querySelector('#Done')
                ToDo.classList.add('hide')
                Doing.classList.remove('hide')
                Doing.classList.add('show');
                Done.classList.add('hide');
            },
            showDone(){
                let ToDo = document.querySelector('#ToDo')
                let Doing = document.querySelector('#Doing')
                let Done = document.querySelector('#Done')
                ToDo.classList.add('hide')
                Doing.classList.add('hide');
                Done.classList.remove('hide')
                Done.classList.add('show');
            },
            editTodo(index){
                this.editStatus = true
                this.todoForm = this.tasks[index];
                this.index = index
            },
            updateTodo(){
                this.tasks[this.index] = this.todoForm;
                this.editStatus = false
                this.todoForm = {
                    task: null,
                    description:  null,
                    time: null,
                    status: 'todo'
                }
            },
            addTodo(){
                this.tasks.push(this.todoForm)
                this.todoForm ={
                    task: null,
                    description:  null,
                    time: null,
                    status: 'todo'
                }
            },
            moveToDoing(index){
                this.tasks[index].status = 'doing';
            },
            cancelTodo(index){
                this.tasks.splice(index, 1);
            },
            moveTodo(index){
                this.tasks[index].status = 'todo';
            },
            moveToDone(index){
                this.tasks[index].status = 'done';
            }

        }
    }
</script>

<style scoped>
    .btn {
        margin-right: 10px;
    }
    ul {
        list-style-type: none;
        padding-left: 0px;
    }
    a {
        cursor: pointer;
    }
    .show {
        display: block;
    }

    .hide {
        display: none;
    }
</style>