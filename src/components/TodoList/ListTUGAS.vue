<template>
<v-main class="list">
    <h3 class="text-h3 font-weight-medium mb-5">To Do List</h3>
    <div class="grid-container">
        <div class="grid-item">
            <v-card width="1200px">
                <v-card-title>
                    <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line hide-details></v-text-field>
                    <v-spacer></v-spacer>
                    <v-btn color="success" dark @click="dialog = true">
                        Tambah
                    </v-btn>
                    
                </v-card-title>
                <v-data-table :headers="headers" :items="todos" :search="search">
                    <template v-slot:[`item.actions`]="{ item }">
                    <v-btn small class="mr-2" @click="showform()">
                        edit
                    </v-btn>
                    <v-btn small @click="delete_item()">
                        delete
                    </v-btn>
                          <v-btn small class="mr-2" @click="showItem(item)"> Show</v-btn>
                    </template>

                    <template v-slot:[`item.priority`]="{ item }">
                    <v-chip
                    v-if="item.priority=='Penting'"
                    class="ma-2"
                    close
                    color="red"
                    text-color="white"
                    
                    >
                        {{ item.priority }}
                        
                    </v-chip>

                    <v-chip
                    v-else-if="item.priority=='Biasa'"
                    class="ma-2"
                    close
                    color="blue"
                    text-color="white"
                    
                    >
                        {{ item.priority }}
                    </v-chip>

                    <v-chip
                    v-else
                    class="ma-2"
                    close
                    color="green"
                    text-color="white"
                    
                    >
                        {{ item.priority }}
                    </v-chip>
                    </template>

                     <template v-slot:[`item.checkbox`]="{ item }">
                   <input type="checkbox" v-model="item.checked" @change="tercek(item)" >
                    </template>
                </v-data-table>
            </v-card>
        </div>
        <div >
            <v-expansion-panels v-show="expandsive">
             <v-expansion-panel>
            <v-expansion-panel-header >
            Expand
             </v-expansion-panel-header>
           
            <v-expansion-panel-content>
             <v-card v-show="show" >
                        <h4 class="text-left">
                           Note
                        </h4>
                        <br>
                             <h5>{{text3}} </h5>
            </v-card>
             </v-expansion-panel-content>
         </v-expansion-panel>
         </v-expansion-panels>
        </div>
    </div>
    <v-dialog v-model="dialog" persistent max-width="600px">
        <v-card>
            <v-card-title>
                <span class="headline">Form Todo</span>
            </v-card-title>
            <v-card-text>
                <v-container>
                    <v-text-field v-model="formTodo.task" label="Task" required></v-text-field>
                    <v-select v-model="formTodo.priority" :items="['Penting', 'Biasa', 'Tidak penting']" label="Priority" required></v-select>
                    <v-textarea v-model="formTodo.note" label="Note" required></v-textarea>
                </v-container>
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="cancel">
                    Cancel
                </v-btn>
                <v-btn color="blue darken-1" text @click="save">
                    Save
                </v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
    <v-dialog v-model="dialog1" persistent max-width="600px">
        <v-card>
            <v-card-title>
                <span class="headline">Form Todo</span>
            </v-card-title>
            <v-card-text>
                <v-container>
                    <v-text-field v-model="formTodo.task" label="Task" required></v-text-field>
                    <v-select v-model="formTodo.priority" :items="['Penting', 'Biasa', 'Tidak penting']" label="Priority" required></v-select>
                    <v-textarea v-model="formTodo.note" label="Note" required></v-textarea>
                </v-container>
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="cancel">
                    Cancel
                </v-btn>
                <v-btn color="blue darken-1" text @click="edit">
                    Save
                </v-btn>
                
            </v-card-actions>
        </v-card>
    </v-dialog>
    
    <v-card v-show="checkedtugas" width="1600" > 
        <v-card-title>
            <h3 class="ml-2">Delete Multiple</h3> 
            <v-spacer></v-spacer>
                    <v-btn color="red" dark @click="delete_all(0)">
                        Delete All
                    </v-btn>
        </v-card-title>
        <div v-for="todo in todos" :key="todo.task">
            <h5 class="ma-2 ml-5" v-if="todo.checked">
                {{todo.task}}
            </h5>
        </div>
    </v-card>

</v-main>
</template>

<script>
export default {
    name: "List",
    data() {
        return {
            search: null,
            dialog: false,
            dialog1: false,
            show: false,
            expandsive: false,
            text1: "",
            text2: "",
            text3: "",
            item1: null,
            index: 0,
            headers: [{
                    text: "Task",
                    align: "start",
                    sortable: true,
                    value: "task",
                },
                {  text: "Priority", value: "priority", },
                {  text: "Actions", value: "actions", },
                {  text: "Check", value: "checkbox", },
            ],
            todos: [{
                    task: "bernafas",
                    priority: "Penting",
                    note: "huffttt",
                    checked: false,
                },
                {
                    task: "nongkrong",
                    priority: "Tidak penting",
                    note: "bersama tman2",
                    checked: false,
                },
                {
                    task: "masak",
                    priority: "Biasa",
                    note: "masak air 500ml",
                    checked: false,
                },
            ],
            
            formTodo: {
                task: null,
                priority: null,
                note: null,
                checked: false,
            },

            checkedtugas: true,
            checked: false,
        };
    },
    methods: {
        tercek(item){
            
                    this.checkedtugas = true;

                this.item1 = item;    
        },

        save() {
            this.todos.push(this.formTodo);
            this.resetForm();
            this.dialog = false;
        },
        cancel() {
            this.resetForm();
            this.dialog = false;
            this.dialog1 = false;
        },
        resetForm() {
            this.formTodo = {
                task: null,
                priority: null,
                note: null,
            };
        },
        showItem(x) {
            this.show = true;
            this.text3 = x.note;
            this.item1 = x;
            this.expandsive = true;
        },
        showform() {
            this.dialog1 = true;
            this.formTodo.task = this.text1;
            this.formTodo.priority = this.text2;
            this.formTodo.note = this.text3;
        },
        edit() {
            this.index = this.todos.indexOf(this.item1);
            this.todos[this.index].task = this.formTodo.task;
            this.todos[this.index].priority = this.formTodo.priority;
            this.todos[this.index].note = this.formTodo.note;
            this.dialog1 = false;
            this.showItem(this.todos[this.index]);
        },
        delete_item() {
            this.index = this.todos.indexOf(this.item1);
            this.todos.splice(this.index, 1);
            this.show = false;
        },
        delete_all(index){
            for (index = 0; index < this.todos.length; index++){
                if(this.todos[index].checked){
                    this.todos.splice(index,1);
                    index=-1;
                }
            }  
        }
    },
};
</script>