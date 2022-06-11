<template>
    <div class="header">
        <h1 class="header__title">
            Keep Your Work Organized
        </h1>
        <div class="header__date">
            <h3 class="week-day">{{dayName}}</h3>
            <span class="date-format">{{currentDate}}</span>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            weekday : ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"],
            date : new Date(),
        }
    },
    computed:{
        dayName(){
            return this.weekday[this.date.getDay()]
        },
        currentDate(){
            return `${this.date.getDate()} - ${this.date.getMonth() +1} - ${this.date.getFullYear()}`;
        },
    },
}
</script>

<style lang="postcss">
    .header{
        height: 180px;
        background-image: url("../assets/clouds.jpg");
        background-size: cover;
        background-position:left;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
        padding-top: 40px;
        &__title{
            font-family:'Lobster Two', cursive;
            font-size:40px;
            color:var(--beige);
            text-align: center;
        }
        &__date{
            display: flex;
            justify-content:center;
            align-items: center;
            color: var(--beige);
            padding-top:10px;
            margin: auto;
        .week-day{
            font-family: var(--app-font-cursive);
            font-size:25px;
            margin-right: 10px;
        }
        .date-format{
            font-family: var(--app-font-normal);
            align-self: flex-end;
            font-size: 18px;
        }
        }
        @media screen and (max-width:637px) {
            height:250px;
      }
    }
</style>