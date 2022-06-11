<template>
    <div>
        <div class="tasks" v-if="!showCompleted">
            <h2 class="tasks__title">You Have <span class="tasks__title__number">{{pendingTasksLength}} </span> Pending Tasks</h2>
            <ul :key="task.id"
                v-for="task in tasks"
                class="tasks__list"
                >
                <li class="tasks__list__item">
                    <i :class="[task.isCompleted ? 'bx bxs-check-circle' : 'bx bx-check-circle']" @click="task.isCompleted = !task.isCompleted"></i>
                    <span :class="{completed:task.isCompleted}">{{task.name}}</span>
                    <i class='bx bxs-trash' @click="$emit('delete')"></i>
                </li>
            </ul>
        </div>
        <div class="tasks" v-show="showCompleted === true">
            <h2 class="tasks__title">You Have <span class="tasks__title__number">{{completedTasksLength}} </span> Completed Tasks</h2>
            <ul :key="task.id"
                v-for="task in completed"
                class="tasks__list"
                >
                <li class="tasks__list__item">
                    <i :class="[task.isCompleted ? 'bx bxs-check-circle' : 'bx bx-check-circle']" @click="task.isCompleted = !task.isCompleted"></i>
                    <span :class="{completed:task.isCompleted}">{{task.name}}</span>
                    <i class='bx bxs-trash' @click="$emit('delete')"></i>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default{
        props:[
                "tasks",
                "completed", 
                "showCompleted", 
                "completedTasksLength", 
                "pendingTasksLength"
            ],
    }
</script>

<style lang="postcss">
    .tasks{
        width:60%;
        margin: 20px auto;    
    &__list{
        list-style-type: none;
        &__item{
            display:grid;
            grid-template-columns: 1fr 10fr 1fr;
            padding: 15px 0;
            font-family: var(--app-font-normal);
            font-size: 16px;
            color:var(--blue);
            border-top:solid 1.5px var(--lighter-blue);
            border-radius: 5px;
            span{
                font-weight: bold;
                text-transform: capitalize;
            }
            i {
                font-size:20px;
                color:var(--blue);
                font-weight: bold;
            }
            .completed{
                text-decoration: line-through;
            }
            .bxs-check-circle{
                color:var(--light-green);
                text-decoration: none;
            }
            .bxs-trash:hover{
                color:var(--red);
            }
        }
    }
    &__title{
        font-family: var(--app-font-cursive);
        padding:0 0 20px 0;
        font-size:25px;
        text-align: center;
        color: var(--dark-blue);
        &__number{
            color:var(--red);
            font-size:30px;
            font-weight: bold;
        }
    }
    }  
</style>