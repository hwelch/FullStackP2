<template>
<v-app id="main-app">
    <v-card>
    <!--panel header-->
        <v-card-title
            class='headline primary pa-0'
            id="primary-title" >
            <div class="row">
                <div class="col-md-6 text-right">
                    <h4>
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-list" viewBox="0 0 16 16">
                            <path fill-rule="evenodd" d="M2.5 12a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5z"/>
                        </svg>
                        FRAMEWORKS
                    </h4>
                </div>

                <div class="col-md-6 text-right">
                    <button class="btn btn-primary" id="addButton" type="button" @click="toggleModal('add')" data-toggle="modal" data-target="#exampleModal">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-circle-fill" viewBox="0 0 16 16">
                            <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM8.5 4.5a.5.5 0 0 0-1 0v3h-3a.5.5 0 0 0 0 1h3v3a.5.5 0 0 0 1 0v-3h3a.5.5 0 0 0 0-1h-3v-3z"/>
                        </svg>
                        ADD
                    </button>
                </div>
            </div>
        </v-card-title>

    <!--panel body-->
        <v-simple-table id="main-panel">
            <template v-slot:default>
            <!--table header-->
                <thead>
                <tr>
                    <th>
                        <div class="text-center">
                        Title
                        </div>
                    </th>

                    <th>
                        <div class="text-center">
                        Description
                        </div>
                    </th>

                    <th>
                        <div class="text-center">
                        Deadline
                        </div>
                    </th>

                    <th>
                        <div class="text-center">
                        Priority
                        </div>
                    </th>

                    <th>
                        <div class="text-center">
                        Is Complete
                        </div>
                    </th>

                    <th>
                        <div class="text-center">
                        Action
                        </div>
                    </th>
                </tr>
                </thead>
            <!--table body-->
                <tbody>
                    <tr v-for="todo in alltodos" :key="todo.title">
                        <td>
                            <div class="text-center">
                            {{todo.title}}
                            </div>
                        </td>

                        <td>
                            <div class="text-center">
                            {{todo.description}}
                            </div>
                        </td>

                        <td>
                            <div class="text-center">
                            {{reformatDate(todo.deadline)}}
                            </div>
                        </td>

                        <td>
                            <div class="text-center">
                            {{todo.priority}}
                            </div>
                        </td>

                        <td>
                            <div class="text-center">
                            <input type="checkbox" id="checkbox" v-model="todo.isComplete" />
                            </div>
                        </td>

                        <td>
                            <div class="text-center">
                                <button class="btn btn-block btn-primary my-btn" id="internalUpdateTaskButton" type="button" @click="toggleModal('update', todo.title)" data-toggle="modal" data-target="#exampleModal" v-if="!todo.isComplete" >
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                                    <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                                    <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
                                    </svg>
                                    Update
                                </button>
                                <button class="btn btn-block btn-danger my-btn" type="button" id="deleteTaskButton" @click="deleteTask(todo.title)">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-circle-fill" viewBox="0 0 16 16">
                                    <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM5.354 4.646a.5.5 0 1 0-.708.708L7.293 8l-2.647 2.646a.5.5 0 0 0 .708.708L8 8.707l2.646 2.647a.5.5 0 0 0 .708-.708L8.707 8l2.647-2.646a.5.5 0 0 0-.708-.708L8 7.293 5.354 4.646z"/>
                                    </svg>
                                    Delete
                                </button>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </template>
        </v-simple-table>
    </v-card>

<!--modal code-->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalTitle" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" >
            <div class="modal-content">
            
                <!-- modal header should have either add or edit task and be same shade of blue --> 
                <div class="modal-header headline primary">
                    <h5 class="modal-title" id="modalHeaderTitle" v-if="header == 'add'">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-circle-fill" viewBox="0 0 16 16">
                            <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM8.5 4.5a.5.5 0 0 0-1 0v3h-3a.5.5 0 0 0 0 1h3v3a.5.5 0 0 0 1 0v-3h3a.5.5 0 0 0 0-1h-3v-3z"/>
                        </svg>
                        Add Task
                    </h5>
                    <h5 class="modal-title" id="modalHeaderTitle" v-else>
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                            <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                            <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
                        </svg>
                        Edit Task
                    </h5>
                </div>

                <!-- all of the info for the body should depend on if the names are empty or full -->
                <div class="modal-body">
                    <div class="container-fluid">
                    <form>
                        <!--title textbox-->
                        <!--title is only shown when it is being added-->
                        <div class="row form-group-extraspace" id="titleDiv" v-if="header == 'add'">
                            <input type="text" class="form-control" id="titleEx"
                                placeholder="Title" v-model="title">
                                <div v-if="titleEmpty" id="internal-div">
                                    <p id="error-message">Title is Required</p>
                                </div>
                                <div v-if="!titleUnique" id="internal-div">
                                    <p id="error-message">Title must be Unique</p>
                                </div>
                            
                        </div>
                        <!--description textbox-->
                        <div class="row form-group-extraspace" id="descriptionDiv">
                            <input type="text" class="form-control" id="descriptionEx"
                                placeholder="Description" v-model="description">
                                <div v-if="descriptionEmpty" id="internal-div">
                                    <p id="error-message">Description is Required</p>
                                </div>
                            
                        </div>
                        <!--deadline datepicker-->
                        <div class="row form-group">
                            <input type="date" class="form-control datepicker" id="checkIn"
                                value="2018-07-22" autocomplete="off" autofill="off" v-model="deadline">
                        </div>
                        <!--priority radio button-->
                        <div class="row">
                                Priority
                        </div>
                        <div class="row radio form-group">
                                <div class="col-md-4">
                                    <input class="form-check-input" type="radio" name="prio" id="inlineRadio1"
                                        value="low" v-model="priority">
                                    <label for="inlineRadio1">Low</label>
                                </div>
                                <div class="col-md-4">
                                    <input class="form-check-input" type="radio" name="prio" id="inlineRadio2"
                                        value="med" v-model="priority">
                                    <label for="inlineRadio2">Med</label>
                                </div>
                                <div class="col-md-4">

                                    <input class="form-check-input" type="radio" name="prio" id="inlineRadio3"
                                        value="high" v-model="priority">
                                    <label for="inlineRadio3">High</label>
                            </div>
                        </div>
                        <!--add/edit and cancel buttons-->
                        <div class="row">
                            <div class="col-md-6">
                                <button class="btn btn-block btn-primary" id="internalUpdateButton" type="button" @click="tryAdding()" v-if="header == 'add'">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-circle-fill" viewBox="0 0 16 16">
                                    <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM8.5 4.5a.5.5 0 0 0-1 0v3h-3a.5.5 0 0 0 0 1h3v3a.5.5 0 0 0 1 0v-3h3a.5.5 0 0 0 0-1h-3v-3z"/>
                                    </svg>
                                    Add
                                </button>
                                <button class="btn btn-block btn-primary" id="internalUpdateButton" type="button" @click="tryUpdating()" v-else>
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                                        <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                                        <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
                                    </svg>
                                    Edit
                                </button>
                            </div>
                            <div class="col-md-6">
                                <button class="btn btn-block btn-danger" type="button" id="cancelButton" data-dismiss="modal">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-circle-fill" viewBox="0 0 16 16">
                                    <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM5.354 4.646a.5.5 0 1 0-.708.708L7.293 8l-2.647 2.646a.5.5 0 0 0 .708.708L8 8.707l2.646 2.647a.5.5 0 0 0 .708-.708L8.707 8l2.647-2.646a.5.5 0 0 0-.708-.708L8 7.293 5.354 4.646z"/>
                                    </svg>
                                    Cancel
                                </button>
                            </div>
                        </div>
                    </form>
                </div>
                </div>
            </div>
        </div>
    </div>

</v-app>
</template>


<script>
//master
    export default {
    //life cycles
        created(){},
    //methods
        methods: {
            toggleModal(type, title) {
                this.header = type
                if (title) {
                    let filtered = this.alltodos.filter(a => a.title==title)[0]
                    this.title = filtered.title
                    console.log(this.title)
                }
                else {
                    this.title = ''
                    this.description=''
                    this.deadline=''
                    this.priority='low'
                    this.isComplete=false
                }
            },
            addTodo() {
                var currTodo = {
                    title: this.title,
                    description: this.description,
                    deadline: this.deadline,
                    priority: this.priority,
                    isComplete: this.isComplete,
                }
                this.alltodos.push(currTodo)
            },
            deleteTask(task) {
                this.alltodos = this.alltodos.filter(function(ele) {
                    return ele.title != task
                })
                toastr.success("Task was deleted successfully")
            },
            validateDialog() {
                //check if the title is empty if it is make the box red
                if (this.title == '') {
                    $("#titleDiv").addClass('has-error')
                    this.titleEmpty = true
                }
                else {
                    $("#titleDiv").removeClass('has-error')
                    this.titleEmpty = false
                }

                //check if the description is empty if it is make the box red
                if (this.description == '') {
                    $("#descriptionDiv").addClass('has-error')
                    this.descriptionEmpty = true
                }
                else {
                    $("#descriptionDiv").removeClass('has-error')
                    this.descriptionEmpty = false
                }
            },
            validateTitle() {
                var index = this.alltodos.indexOf(this.alltodos.filter(a => a.title==this.title)[0]);
                if(index == -1) {
                    this.titleUnique = true
                }
                else {
                    this.titleUnique = false
                }
                console.log(this.titleUnique)
            },
            updateTodo() {
                var index = this.alltodos.indexOf(this.alltodos.filter(a => a.title==this.title)[0]);
                this.alltodos[index].description= this.description,
                this.alltodos[index].deadline= this.deadline,
                this.alltodos[index].priority= this.priority,
                this.alltodos[index].isComplete= this.isComplete
            },
            tryAdding() {
                this.validateDialog()
                this.validateTitle()
                if(!this.titleEmpty && !this.descriptionEmpty && this.titleUnique) {
                    this.addTodo()
                    $('#exampleModal').modal('hide')
                    toastr.success("Task was added successfully")
                }
            },
            tryUpdating() {
                this.validateDialog()
                if(!this.descriptionEmpty) {
                    this.updateTodo()
                    $('#exampleModal').modal('hide')
                    toastr.success("Task was updated successfully")
                }
            },
            reformatDate(dateInfo) {
                if (dateInfo == "" || dateInfo == undefined) {
                    let today = new Date();
                    let yyyy = today.getFullYear();
                    let mm = today.getMonth() + 1; // Months start at 0!
                    let dd = today.getDate();
                    return mm + "/" + dd + "/" + yyyy
                }
                let arr = dateInfo.split("-")
                return arr[1] + "/" + arr[2] + "/" + arr[0]
            }
        }, 
    //watchers
        watch: {},
    //computed
        computed: {},
    //global vars
          data: global => ({
            title:'',
            description:'',
            deadline: '',
            priority:'low',
            isComplete:false,
            header:'',
            alltodos: [],
            titleEmpty:false,
            descriptionEmpty:false,
            titleUnique:true
        }),
    }
</script>

<style scoped >
    #addButton {
        margin-right: 3%;
        height:100%;
        width:15%;
    }

    #primary-title {
        color:white;
    }

    #modalHeaderTitle {
        color:white;
    }

    .my-btn {
        height:100%;
        width:50%;
    }

    .modal-dialog {
        width:20%;
    }

    .form-group {
        margin-bottom: 5%;
    }

    .form-group-extraspace {
        margin-bottom: 10%;
    }

    #main-panel {
        margin: 20px;
    }

    #main-app {
        margin:30px;
    }

    #error-message {
        font-size:xx-small;
        margin-left:5%;
        color:red;
    }

    #internal-div {
        width: 100%;
    }
    
</style>