<template>
  <div class="uk-container uk-container-expand">
    <div class="uk-flex uk-flex-center">
    <password-composition />
    <password-options />

    </div>
</div>
</template>

<script>
import PasswordOptions from './components/PasswordOptions.vue'
import PasswordComposition from './components/PasswordComposition.vue'


export default {
  components: { PasswordComposition, PasswordOptions }
}

</script>

<style>
.setting {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin: 15px 0;
}
body {
  background-color: rgb(35, 88, 158);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
