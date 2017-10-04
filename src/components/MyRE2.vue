<template>
  <div>
    <input v-model="newItem" @keyup.enter="checkItem">
    <button @click="checkItem">Tester une phrase</button>
    <!--displays list -->
    <ul id='bad'>
      <li class='listitem' v-for="item in badItems">{{ item }}</li>
    </ul>
    <ul id='good'>
      <li  class='listitem' v-for="item in goodItems">{{ item }}</li>
    </ul>
    <p>commence avec un des mots suivants:</p>
    <ul>
      <li  class='listitem' v-for="item in listItems">{{ item }}</li>
    </ul>
    <input v-model="newWord"  @keyup.enter="setWord">
    <button @click="setWord">Ajouter un mot</button>

    <button @click="resetWords">Reset</button>

  </div>
</template>

<script>
export default {
  data () {
    return {
      listItems: ['Die', 'Das', 'Der'],
      goodItems: [],
      badItems: [],
      newItem: '',
      newWord: ''
    }
  },
  methods: {
    setWord () {
      this.listItems.push(this.newWord)
      this.newWord = ''
    },
    resetWords () {
      this.listItems = []
      this.badItems = []
      this.goodItems = []
    },
    checkItem () {
      console.log('Running')
      var r = this.newItem
      var score = 0
      var a = r.split(' ')
      for (let j = 0; j < a.length; j++) {
        if (a[j] === '') {
          throw Error('Le string de RE est vide')
        } else {
          console.log('else ' + this.listItems.length)
          for (let i = 0; i < this.listItems.length; i++) {
            var toTest = this.listItems[i] + '(?![A-Za-z])'
            var re = new RegExp(toTest)
            if (re.test(a[j])) {
              score += 1
            }
          }
        }
        console.log(a, score)
      }
      console.log(score, a.length)
      if (score === a.length) {
        this.propValue = this.newItem
        this.goodItems.push(this.newItem)
      } else {
        this.propValue = ''
        this.badItems.push(this.newItem)
      }
      this.newItem = ''
      score = 0
    }
  }

}
</script>
<style>
.listitem {
    list-style: none;
    padding: 16px 16px 16px 60px;
    border: 10px;
    background: rgba(0, 0, 0, 0.003);
    box-shadow: inset 0 -2px 1px rgba(0,0,0,0.03);
}
#bad {
  text-decoration: line-through;
  color : red;
}
#good {
  color : green;
}

</style>
