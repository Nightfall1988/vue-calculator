<template>
<div>
  <form action="/" @submit.prevent = "onSubmit">
    <input type="text"  :value="firstNum" @input='setFirstNum($event)' name='firstNum'>
    <input type="text"  :value="secondNum" @input='setSecondNum($event)' name='secondNum'>
    <br>
    <div id='operations'>
    <button class='bttn' id='add' @click="add(firstNum, secondNum)">+</button>
    <button class='bttn' id='subtract' @click="subtract(firstNum, secondNum)">-</button>
    <button class='bttn' id='multiply' @click="multiply(firstNum, secondNum)">*</button>
    <button class='bttn' id='divide' @click="divide(firstNum, secondNum)">/</button>
    </div>
  </form>
<button id='filter' @click="show()"> Filter </button>
<div id='result'>
<p>Result: {{ result }}</p>
</div>
<div id='historyList' v-for="(item, i) in list" :key="i">
  {{ item[0] }} {{ item[3] }} {{ item[1] }} = {{ item[2] }} 
<br>
</div>
<br>
<div id='filterColumns' ref="columns" v-bind:style="{ display: activeDisplay}">
  <div id='positiveColumn' style="margin-right: 10px;">
    <p style="font-weight: bold;">Positive values:</p>
    <div>
      <div id='positiveVal' v-for="(pNum, i) in positive" :key="i">
        {{ pNum }}<br>
      </div>
    </div>
  </div>
  <div id='negativeColumn'>
    <p style="font-weight: bold;">Negative values:</p>
    <div>
      <div id='negativeVal' v-for="(nNum, i) in negative" :key="i">
        {{ nNum }}<br>
      </div>
    </div>
  </div>
</div>

</div>
</template>

<script>
export default {
  data() {
    return {
      firstNum: '',
      secondNum: '',
      history: [],
      histiryInstance: [],
      result: '',
      list: [],
      negative: [],
      positive: [],
      index: '',
      activeDisplay: 'none'
    }
  },

  methods: {

    setFirstNum(event) {
      this.firstNum = parseInt(event.target.value)
    },

    setSecondNum(event) {
      this.secondNum = parseInt(event.target.value)
    },

    add: function(firstNum, secondNum) {
      this.result = firstNum + secondNum
      this.historyInstance = [firstNum, secondNum, this.result, ' + ']
      this.addItemToHistory(this.historyInstance)
      this.filter(this.list)
    },

    subtract: function(firstNum, secondNum) {
      this.result = firstNum - secondNum
      this.historyInstance = [firstNum, secondNum, this.result, ' - ']
      this.addItemToHistory(this.historyInstance)
      this.filter(this.list)
    },
    
    multiply: function(firstNum, secondNum) {
      this.result = firstNum * secondNum
      this.historyInstance = [firstNum, secondNum, this.result, ' * ']
      this.addItemToHistory(this.historyInstance)
      this.filter(this.list)
    },

    divide: function(firstNum, secondNum) {
      this.result = firstNum / secondNum
      this.historyInstance = [firstNum, secondNum, this.result, ' / ']
      this.addItemToHistory(this.historyInstance)
      this.filter(this.list)
    },

    addItemToHistory: function(historyInstance) {
      if (this.historyInstance[2]) {
        this.list.push(historyInstance)
      }
    },

    filter: function(list) {
      this.index = list.length-1
      if (list[this.index][2] >= 0) {
        this.positive.push(list[this.index][2])
      } else {
        this.negative.push(list[this.index][2])
      }
    },

    show: function() {
      this.activeDisplay = 'flex'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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

#operations {
  display: flex;
  justify-content: center;
}

.bttn {
  border-radius: 3px;
  margin: 10px;
  width: 40px;
  height: 30px;
  font-size: 20px;
  font-weight: bold;
  }

#add {
  background-color: rgb(71, 235, 218);
}

#subtract {
  background-color: rgb(112, 224, 64);
}

#multiply {
  background-color: rgb(200, 64, 224);
}

#divide {
  background-color: rgb(224, 141, 64);
}

#filter {
  background-color: rgb(23, 30, 107);
  color: rgb(255, 255, 255);
  border-radius: 3px;
  margin: 10px;
  width: 70px;
  height: 30px;
  font-size: 20px;
  font-weight: bold;
}

#filterColumns {
  justify-content: center;
  flex-direction: row;
}
</style>
