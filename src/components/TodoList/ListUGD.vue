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
                </v-data-table>
            </v-card>
        </div>
        <div class="grid-item">
            <v-expansion-panels>
             <v-expansion-panel>
            <v-expansion-panel-header >
            Expand
             </v-expansion-panel-header>
           
            <v-expansion-panel-content>
             <v-card v-show="show" >
              <v-simple-table >
                  <table>
                      <thead>
                        <tr>
                        <th class="text-left">
                            Task
                        </th>
                        <th class="text-left">
                            Priority
                        </th>
                        <th class="text-right">
                            Note
                        </th>
                        </tr>
                        </thead>
                         <tbody>
                             <td>{{text1}} </td>
                             <td>{{text2}} </td>
                             <td>{{text3}} </td>
                         </tbody>
                 
                  </table>
              </v-simple-table>
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
                { text: "Priority", value: "priority",
                },
                { text: "Note",value: "note",
                },
                {  text: "Actions", value: "actions", },
            ],
            todos: [{
                    task: "bernafas",
                    priority: "Penting",
                    note: "huffttt",
                },
                {
                    task: "nongkrong",
                    priority: "Tidak penting",
                    note: "bersama tman2",
                },
                {
                    task: "masak",
                    priority: "Biasa",
                    note: "masak air 500ml",
                },
            ],
            formTodo: {
                task: null,
                priority: null,
                note: null,
            },
        };
    },
    methods: {
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
            this.text1 = x.task;
            this.text2 = x.priority;
            this.text3 = x.note;
            this.item1 = x;
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
    },
};
</script>