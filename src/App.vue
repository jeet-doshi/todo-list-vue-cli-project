<template>
    <body>
       <div class="block" id="app">   
            <div class="container">
                <h1 class="heading">To-Do App</h1>
                <label style="font-weight: bold;">New To-Do</label>
                <br>
<!-- Input Box --> <input type="text" placeholder="Please enter an activity" id="name"  class="input-box" v-model="todo" /> 
                  <h5 v-if="isError">*Please enter a value</h5>
<!-- Input Box for num -->  <input type="text" placeholder="Please enter todo number according to priority" class="input-box" @keypress="validateNumber" v-model="priority" /> 
                  <h5 v-if="isErrorNum">*Please enter a number</h5> 
                
<!-- Button    --> <input type="button" value="Add ToDo" id="btn-click" class="btn" @click="storeTodo"  />
<!-- Initial Display List -->
                <h2 class="sub-heading">To-Do List</h2>
                <hr size="1" width="100%" color="white">
<!-- Display Div -->
                <ul id="box">
                    <li v-for="(todo, index) in todos" :key="index">
                        <!-- {{ todo.seq }} -  -->
                        {{ todo.seq }} -
                        {{ todo.name }}
                       
                        <button @click="deleteTodo(index)" class="remove-btn">Remove</button>
                    </li>
                </ul>
<!-- Removed List item -->
              <h2 class="sub-heading" style="margin-top: 40px;">Completed List</h2>
                <hr size="1" width="100%" color="white">
<!-- Display Div --><ul id="box">
                    <li v-for="(todo, index) in removedTodos" :key="index" >
                       <div class="strikeout">
                          {{ todo.seq }} -
                          {{ todo.name }}
                       </div> 
                       <div style="display: flex;  ">
                          <button class="remove-btn" @click="undoTodo(index)">Undo</button>
                          <button class="remove-btn delete-btn" @click="clearTodo(index) ">Delete</button>
                        </div>
                    </li>
                </ul>
                
            </div>
        </div>


    </body>
</template>

<script>    
export default {
  name: 'app',

    // el: '#app',

    data() {
        return{
        todo: '',
        todos: [],
        isError: false,
        priority: "",
        priorities: [],
        isErrorNum: false,
        removeTodo: "",
        removedTodos: [],
      };
    },

    methods: {

   validateNumber()
        {
         
          let keyCode = event.keyCode;
          if(keyCode < 48 || keyCode > 57)
          {
            event.preventDefault();
            this.isErrorNum = true
          }
          else{
            this.isErrorNum = false
          }
        },

        storeTodo() {
            if(this.todo!=""){
                this.todos.push({
                  name: this.todo,
                  seq: Number(this.priority),
                  isStrikedOff: false
                });
            // sort the this.todos array
              this.todos.sort( (a, b) => { return a.seq - b.seq })
            // sort array complete
                this.todo = "";
                this.priority = "";
                this.isError= false
            } else {
                this.isError= true 
            }          
        },

        deleteTodo(index) {
          this.removedTodos.push(...this.todos.splice(index, 1));
        },

        clearTodo(index) {
          this.removedTodos.splice(index, 1)
        },

        undoTodo(index) {
          this.todos.push(...this.removedTodos.splice(index, 1));
        }

   }

  }  

</script>

<style>
.block {
  padding: 5px;
  border: 1.5px solid rgb(1, 1, 1);
  width: 450px;
  margin: auto;
  background-color: #190926;
  border-radius: 5px;
}

.container {
  color: white;
  padding: 5px;
  /* border-bottom: 2px solid white; */
  width: 95%;
  margin: auto;
  background-color: #190926;
  padding-bottom: 0px;
}

.heading {
  color: white;
  margin: 20px;
  margin: 10px;
  text-align: center;
}

.input-box {
  width: 95%;
  height: 30px;
  margin-top: 5px;
  margin-bottom: 5px;
  border-radius: 10px;
  border: 1.7px solid white;
  background-color: #190926;
  color: white;
}

.btn {
  width: 97%;
  height: 27px;
  margin-bottom: 10px;
  margin-top: 5px;
  background-color: #d13db7;
  border-radius: 10px;
  border: 2px solid white;
  color: white;
  font-weight: bold;
}

.btn:hover {
  cursor: pointer;
  background-color: #fffaf0;
  color: #190926;
  transition-duration: 500ms;
}

/* .container-two {
  margin-top: 0px;
  height: 70%;
  border-bottom: none;
  color: white;
}

#error {
  color: red;
  font-size: 14px;
} */

/*  Display List  */

ul {
  list-style-type: none;
  padding-left: 0px;
}

.remove-btn {
  margin-right: 15px;
  background-color: #d13db7;
  border-radius: 3px;
  border: 1px solid white;
  color: white;
  font-size: 12px;
}

.remove-btn:hover {
  cursor: pointer;
  background-color: #fffaf0;
  color: #190926;
  font-weight: bold;
}

li {
  font-size: 14;
  border: white solid 1px;
  border-radius: 5px;
  margin-bottom: 10px;
  padding: 4px;
  display: flex;
  justify-content: space-between;
}

h5 {
  margin-top: 0px;
  color: red;
}

.strikeout {
  text-decoration: line-through;
}

.delete-btn {
  background-color: rgba(240, 12, 12, 0.7);
  color: whitesmoke;
}

.delete-btn:hover {
  background-color: white;
  color: black;
}

.sub-heading {
  margin-bottom: 0px;
   color: #d13db7;
}

</style>
