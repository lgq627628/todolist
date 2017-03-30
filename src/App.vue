<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model='newItem' @keyup.enter='addNew' placeholder="What needs to be done?">
    <ul>
      <li v-for='item in items' :class='{finished: item.isFinished}' v-on:click='toggleFinished(item)'>
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store'

export default {
  data: function(){
    return {
      title: 'todos',
      items: Store.fetch(),
      newItem: '',
    }
  },

  methods: {
    toggleFinished: function(item){
      console.log(item.isFinished = !item.isFinished)
    },
    addNew: function(){
      if(this.newItem) this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem=''
    }
  },

  watch: {
    items: {
      handler: function(items){
        Store.save(items)
      },
      deep: true
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  background: rgb(245,245,245);
}
#app{
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  background: rgb(245,245,245);
  position: relative;
}
#app h1{
  font-size: 100px;
  font-weight: 100;
  padding-top: 20px;
  text-align: center;
  color: rgba(175, 47, 47, 0.15);
}
#app input{
  position: relative;
  margin-bottom: 10px;
  width: 40%;
  font-size: 24px;
  line-height: 1.4em;
  outline: none;
  background: #fff;
  padding: 16px 16px 16px 20px;
  border: none;
  box-shadow: 0 5px 12px 3px rgba(0, 0, 0, 0.2)
}
#app li{
  list-style:none;
  font-size:1.6em;
  margin-top:10px;
  position: relative;
  font-size: 24px;
  border-bottom: 1px solid #ededed;
}
.finished {
  text-decoration: line-through;
}

</style>
