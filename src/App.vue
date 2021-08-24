<template>
    <body>
       <div class="block" id="app">   
            <div class="container">
                <h2 class="heading">To-Do App</h2>
                <label style="font-weight: bold;">New To-Do</label>
                <br>
<!-- Input Box --> <input type="text" placeholder="Please enter an activity" id="name"  class="input-box" v-model="todo" /> 
                  <h5 v-if="isError">*Please enter a value</h5>
<!-- Input Box for num -->  <input type="text" placeholder="Please enter todo number according to priority" class="input-box" @keypress="validateNumber" v-model="priority" /> 
                  <h5 v-if="isErrorNum">*Please enter a number</h5> 
                
<!-- Button    --> <input type="button" value="Add ToDo" id="btn-click" class="btn" @click="storeTodo"  />
                <!-- <h5 v-if="isError">*Please enter a value</h5> -->
                <!-- <span id="error"></span> -->
                <h3>To-Do List</h3>
                <hr size="1" width="100%" color="white">
<!-- Display --><ul id="box">
                    <li v-for="(todo, index) in todos" :key="index">
                        <div class="itemPriority" v-for="(priority, index) in priorities" :key="index">
                            {{ priority.name }}
                      </div>
                        {{ todo }}

                        <button @click="deleteTodo(index)" class="remove-btn">Remove</button>
                    </li>
                </ul>
            </div>
        </div>

    <!-- <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12"></script>  -->
        <!-- <script src="Vue JS/vue.js"></script>
        <script src="script.js"></script> -->

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
        isErrorNum: false
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
                this.todos.push(this.todo);
                this.todo = "";
                this.priorities.push({name: this.priority});
                this.priority = "";
                this.isError= false
            } else {
                this.isError= true 
            }          
        },


    // change:function(e){
    //   const number = e.target.value
    //   this.isNumberValid(number);
    // },
    // isNumberValid: function(inputNumber) {
    //   this.isValid=   this.regex.test(inputNumber)
    // },

        deleteTodo(index) {
            this.todos.splice(index, 1)
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

</style>
