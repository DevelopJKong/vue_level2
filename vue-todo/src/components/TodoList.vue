<template>
  <div>
  <ul>
    <!-- v-bind:key는 vscode에서만 발생하는 오류 이기 때문에 굳이 사용하지 않아도 된다-->
    <li v-for="(todoItem,index) in todoItems" v-bind:key="todoItem.item" class="shadow"> 
      <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed }"></i>
      <span v-bind:class="{textCompleted: todoItem.completed}">  {{ todoItem.item }}</span>
      <span class="removeBtn" v-on:click="removeTodo(todoItem,index)"><i class="fas fa-trash-alt"></i></span>
    </li>
  </ul>
  </div>
</template>

<script>
export default {
  data : function() {
    return {
      todoItems: []
    }
  },
  methods: {
    removeTodo: function(todoItem, index) {
      console.log(todoItem,index);
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    },
    toggleComplete: function(){
      todoItem.completed = !todoItem.completed;
      //로컬 스토리지에서 갱신하는 로직
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }

  },


  //훅이라고 하는것은 생성되는 시점에 로직이 한번 호출 되는것을 말한다
  created: function() {
    if(localStorage.length > 0) {
        for(var i = 0; i < localStorage.length ; i ++) {
          if(localStorage.key(i) !== 'loglevel:webpack-dev-server') {
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            //this.todoItems.push(localStorage.key(i));
            }

        }
    }
  }
}
</script>

<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
  }

  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
  }    

  .checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-left: 5px;
  }

  .checkBtnCompleted {
    color: #b3adad;
  }

  .textCompleted {
    text-decoration: line-through;
    color:#b3adad;
  }

  .removeBtn {
    margin-left: auto;
    color:#de4343;
  }
</style>