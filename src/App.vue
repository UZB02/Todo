<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="container">
      <nav>
        <RouterLink to="/table1" class="btn">Table1</RouterLink>
        <RouterLink to="/table2" class="btn">Table2</RouterLink>
        <RouterLink to="/test1" class="btn">Test1</RouterLink>
        <RouterLink to="/test2" class="btn">Test2</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  width: 100%;
  background-color: #fff;
  position: sticky;
  top: 0;
  z-index: 111;
  box-shadow: 0 0 15px 10px aliceblue;
}

header .container {
  width: 1200px;
  margin: 0 auto;
  /* background-color: aqua; */
  padding: 10px;
}

header .container nav {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;

}
header .container nav .btn{
  background-color:lime;
  /* width: 70px; */
  padding: 5px 20px;
  text-align: center;
  color: #fff;
  text-decoration: none;
  font-size: 1.2em;
  border-radius: 5px;
  border: 2px solid lime;
  filter: drop-shadow(1px 1px 3px #aaa);
  transition: all .2s ease-in;
}
header .container nav .btn:active{
  border: 2px solid #fff;
}
header .container nav .btn:hover{
  transform: scale(.96);
}
</style>
