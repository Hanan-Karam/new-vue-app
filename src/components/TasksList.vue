<template>
    <div>
        <div class="form">
            <input 
            type="text" 
            v-model="taskName" 
            placeholder="Add A New Task..."
            @keyup.enter="addNewTask"
            >
            <i class='bx bxs-plus-circle' @click="addNewTask"></i>
        </div>
        <p class="message">{{message}}</p>
        <div class="btns">
            <button  @click="toggleCompleted">
                <span v-if="!showCompleted">View Completed Tasks</span>
                <span v-else>View All Tasks</span>
            </button>
            <button class="clear" @click="clearAllTasks">Clear All Tasks</button>
        </div>
        <task-item
            :tasks = "tasks"
            :completed = "completed"
            :showCompleted = "showCompleted"
            :completedTasksLength = "completedTasksLength"
            :pendingTasksLength = "pendingTasksLength"
            @delete="removeTask(index)"
        >
        </task-item>
    </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";
let id = 0;
export default{
    name: "TasksList",
    components:{
        TaskItem,
    },
    data(){
        return{
            taskName: "",
            tasks:[
            ],
            taskData:{
                    id: id++,
                    name: this.taskName,
                    isCompleted: false
            },
            showCompleted : false,
            message: '',
        }
    },
    methods:{
        addNewTask(){
            if(this.taskName){
            // console.log(this.tasks.some(task => task.name === this.taskName))
                if(this.tasks.some(task => task.name.toLowerCase() === this.taskName.toLowerCase())){
                    this.message = "This task is already exist"
                    this.taskName="";
                }else{
                    this.tasks = [{...this.taskData, name: this.taskName}, ...this.tasks]
                    this.taskName="";
                    this.message=""
            }
        }
        },
        removeTask(index){
            this.tasks.splice(index, 1)
        },
        clearAllTasks(){
            this.tasks = [];
        },
        toggleCompleted(){
            this.showCompleted = !this.showCompleted;
        },
    },
    computed:{
        pendingTasksLength(){
            return this.tasks.filter(task => task.isCompleted === false).length
        },
        completedTasksLength(){
            return this.tasks.filter(task => task.isCompleted === true).length
        },
        completed(){
            return this.tasks.filter(task => task.isCompleted === true)
        },
    },
    watch:{
        tasks:{
            handler(){
            localStorage.setItem('todos', JSON.stringify(this.tasks));
        },
        deep: true,
        },
    },
    mounted(){
        this.tasks= JSON.parse(localStorage.getItem('todos')) || [];
    }
}
</script>

<style lang="postcss">
    .form, .btns{
        display: flex;
        justify-content:center;
        align-items: center;
        color:var(--beige);
        padding-top:10px;
        margin: auto;
    }
    .form{
      width:60%;
      color:var(--blue);
      padding-bottom:10px;
        input{
            width: 300px;
            padding:10px 25px;
            border: none;
            display: inline-block;
            margin-right: 10px;
            border-radius: 20px;
            font-family: var(--app-font-normal);
            font-size: 16px;
            color:var(--blue);
            background-color: var(--input-bg);
            border: solid 2px var(--input-bg);
        }
        input:focus{
            background-color: transparent;
            border:solid 2px var(--blue);
        }
        i{
            font-size:40px;
        }
         i:hover{
            color:var(--dark-blue);
        }
    }
    .btns{
        width:70%;
        justify-content: space-around;
         button{
            width: 200px;
            padding:10px 10px;
            border:none;
            font-family: var(app-font-normal);
            font-size:16px;
            border-radius: 15px;
            background-color: var(--blue);
            color:var(--beige);
        }
        button:hover{
            background-color: var(--dark-blue);
        }
        .clear{
            background-color: var(--blue);
            margin-left:10px;
        }
        .clear:hover{
            background-color: var(--red);
        }
        @media screen and (max-width:1334px) {
              width:65%;
      }
        @media screen and (max-width:637px) {
              width: 90%;
              flex-direction: column;
              gap: 10px;
      }
    }
    .message{
        font-family: var(--app-font-normal);
        font-size: 15px;
        color:var(--red);
        text-align: center;
        font-style: italic;
    }
</style>