<template lang='pug'>
  div
    p input names at here, devided by comma
    el-input(v-model="peopleString")
    router-link(:to="{name: 'run', query: {p: peopleString}}")
      el-button(type="primary") go
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      peopleString: 'name1,name2,name3,name4',
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  /* color: #42b983; */
}
.person {
  height:250px;
}
.person-button {
  font-size: 300%;
  width:300px;
  height:200px;
}
.person-button-back {
  margin-left:auto;
  margin-right:auto;
  width:300px;
  height:200px;
  border: #000 solid 1px
}
.red
{
  font-weight: bold;
}
</style>
