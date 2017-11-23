<template lang='pug'>
  .hello
    div(v-if="loading")
      h1 loading....
    div(v-else)
      div.person(v-for="(person,index) in people", :key="index")
        div.person-button-back(v-if="index==selected" @click="selected = -1")
          span {{person}}, you are the secret santa of
          span.red {{giftMap[person]}}
          span please click this button again to hide this secret.
        el-button.person-button(type="danger" v-else-if="disabledItem[index]") {{person}}
        el-button.person-button(type="primary" @click="clickOnPerson($event, index)" v-else) {{person}}
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      people: [],
      disabledItem: {},
      selected: -1,
      giftMap: {},
      loading: true,
    }
  },
  created () {
    this.people = this.$route.query.p.split(',')
    this.getRandom()
  },
  methods: {
    clickOnPerson (event, index) {
      if (this.selected >= 0) {
        this.selected = -1
        return
      }
      // console.log(event, this.people[index])
      this.selected = index
      this.disabledItem[index] = 1
    },
    getRandom () {
      this.$http.get(`https://www.random.org/sequences/?min=0&max=${this.people.length - 1}&col=1&format=plain&rnd=new`).then((response) => {
        let numbers = response.body.split('\n').slice(0, this.people.length)
        // console.log(numbers)
        for (let i in numbers) {
          if (numbers[i] === i) {
            console.log('wrong')
            this.getRandom()
            return
          }
        }
        let m = {}
        for (let i in this.people) {
          m[this.people[i]] = this.people[numbers[i]]
        }
        this.giftMap = m
        this.loading = false
        console.log('finish')
        // console.log(this.giftMap)
      })
    }
  }
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
  color: #42b983;
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
