<template>
  <div class="app">
    <div class="app__container">
      <Header></Header>
      <tasks-list></tasks-list>
    </div>
  </div>
</template>

<script>
import TasksList from "./components/TasksList.vue";
import Header from "./components/Header.vue";
export default {
  name: "App",
  components: {
    TasksList,
    Header,
    Header
},
};
</script>
<style lang="postcss">
  @import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;0,900;1,900&family=Lobster+Two:ital,wght@0,400;0,700;1,400&display=swap');
  *{
    padding:0;
    margin:0;
    box-sizing: border-box;
  }
  :root{
    --dark-blue:#0D335D;
    --blue: #1A508B;
    --lighter-blue:#5584AC;
    --red:#D82148;
    --light-green: #6EBF8B;
    --input-bg:#E9D5CA;
    --beige: #FFF3E6;
    --app-font-cursive:'Lobster Two', cursive;
    --app-font-normal:'Lato';
  }
  .app{
      width: 100%;
      height: 100vh;
      background: linear-gradient(to top , rgba(13, 51, 93, 0.9), rgb(193, 172, 149)) ;
      display:flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      &__container{
          width:40%;
          margin:auto;
          background-color:var(--beige);
          box-shadow: rgba(100, 100, 100, 0.6) 0px 13px 27px -5px, rgba(0, 0, 0, 0.6) 0px 8px 16px -8px;
          border-radius: 10px;
          padding-bottom: 20px;
          @media screen and (max-width:1334px) {
              width: 90%;
              height: 80%;
      }
         @media screen and (max-width:637px) {
              width: 90%;
              height: 90%;
      }
      }
    }
</style>
-