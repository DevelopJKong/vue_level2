 <template>
  <div class="inputBox shadow">
      <!-- template에 들어가는 태그는 하나만 존재할수있다 -->
      <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
      <span class="addContainer" v-on:click="addTodo">
        <i class="fas fa-plus"></i>
      </span>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function(){
      if(this.newTodoItem !== '') {
        var obj = { complete:false, item: this.newTodoItem}
        localStorage.setItem(this.newTodoItem ,JSON.stringify(obj));
        // this를 사용하게 되면 같은 인스턴스에서 
        this.clearInput();
      }
 

    
    },
    
    clearInput: function() {
      this.newTodoItem = ''; 
    }

  }
}
</script>

<!--왜 꼭 이렇게 scoped를 넣어주어야하는지 모르겠다 -->
<style scoped>
  input:focus {
    outline:none;
  }

  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }

  .inputBox input {
    border-style: none;
    font-size: 0.9rem;
  }

  .addContainer {
    float: right;
    background: linear-gradient(to right,#6478F8,#8763FB);
    display:block;
    width:3rem;
    border-radius: 0 5px 5px 0;
  }

  .addBtn {
    color: white;
    vertical-align: middle;
  }
</style>