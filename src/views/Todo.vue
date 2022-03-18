<template>
  <div class="app-body">
    <div class="todo-app">
      <section class="todo-app-box">
        <header class="header">
          <h1>todos</h1>
          <div class="toggle-all" v-on:click="selAll()">▼</div>
          <input
            class="new-todo"
            v-model="valueInput"
            @keyup.enter="keyup_submit()"
            placeholder="What needs to be done?"
          />
        </header>
        <section class="main">
          <ul class="todo-list">
            <li class="todo" v-for="(item, i) in todoList" :key="i">
              <div
                class="view"
                v-if="item.todoIndex === state || showAll === true"
              >
                <input
                  type="checkbox"
                  class="toggle"
                  v-model="item.todoIndex"
                  @change="check(item)"
                />
                <label :class="item.todoIndex === true ? 'del-line' : ''">{{
                  item.todoValue
                }}</label>
              </div>
            </li>
          </ul>
        </section>
        <footer class="footer" v-if="todoList.length > 0">
          <span class="todo-count"
            ><strong>{{ todoList.length }}</strong> item left
          </span>
          <ul class="filters">
            <li><a href="#/all" v-on:click="show(1)">All</a></li>
            <li><a href="#/active" v-on:click="show(2)">Active</a></li>
            <li><a href="#/completed" v-on:click="show(3)">Completed</a></li>
          </ul>
          <button class="clear-completed" @click="clear()">
            Clear completed
          </button>
        </footer>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "Vue-Todo!",
      valueInput: null,
      todoList: [],
      state: false,
      showAll: true,
    };
  },
  methods: {
    //顶部输入框添加事件
    keyup_submit() {
      if (this.valueInput) {
        const todoItem = {
          todoIndex: false,
          todoValue: this.valueInput,
        };
        this.todoList.unshift(todoItem);
        this.valueInput = null;
      }
    },
    //全选操作
    selAll() {
      const r = this.todoList.filter(function (x) {
        return x.todoIndex === false;
      });
      if (r.length === 0) {
        this.todoList.forEach((element) => {
          element.todoIndex = false;
        });
      } else {
        this.todoList.forEach((element) => {
          element.todoIndex = true;
        });
      }
    },
    //删除选中项
    clear() {
      for (let i = 0; i < this.todoList.length; i++) {
        if (this.todoList[i].todoIndex) {
          this.todoList.splice(i, 1);
          i--;
        }
      }
    },
    //选中事件监听
    check(e) {
      console.log(e);
    },
    //展示方法
    show(e) {
      console.log(e);
      if (e === 1) {
        this.showAll = true;
      } else if (e === 2) {
        this.showAll = false;
        this.state = false;
      } else if (e === 3) {
        this.showAll = false;
        this.state = true;
      }
    },
  },
};
</script>
<style scoped lang="less">
.app-body {
  width: 100vw;
  height: 100vh;
  margin: 0;
  overflow-y: auto;
  background-color: #f5f5f5;
}
.todo-app {
  min-width: 230px;
  max-width: 550px;
  margin: 0 auto;
  color: #4d4d4d;
  font-weight: 300;
  font-size: 14px;
  line-height: 1.4em;
  background-color: #fff;
}
.todo-app-box {
  position: relative;
  margin: 130px 0 40px;
  background-color: #fff;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}
.todo-app h1 {
  position: absolute;
  top: -90px;
  width: 100%;
  color: rgba(175, 47, 47, 0.15);
  font-weight: 100;
  font-size: 100px;
  text-align: center;
  text-rendering: optimizeLegibility;
}
.todo-app .new-todo {
  padding: 16px 16px 16px 60px;
  background: rgba(0, 0, 0, 0.003);
  box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
}
.new-todo,
-edit {
  position: relative;
  box-sizing: border-box;
  width: 100%;
  margin: 0;
  padding: 6px;
  color: inherit;
  font-weight: inherit;
  font-size: 24px;
  font-family: inherit;
  line-height: 1.4em;
  border: 0;
  box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
  -webkit-font-smoothing: antialiased;
}
.toggle-all {
  position: absolute;
  z-index: 9;
  margin: 25px;
  color: rgba(0, 0, 0, 0.4);
  cursor: pointer;
}
.todo-list {
  margin: 0;
  padding: 0;
  list-style: none;
}
.todo-list li {
  position: relative;
  font-size: 24px;
  border-bottom: 1px solid #ededed;
}
.todo-list li:last-child {
  border-bottom: 0;
}
.toggle {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 40px;
  height: auto;
  margin: auto 0;
  margin-left: 5px;
  text-align: center;
  border: 0;
}
.todo-list li label {
  display: block;
  padding: 15px 15px 15px 60px;
  line-height: 1.2;
  word-break: break-all;
  transition: color 0.4s;
}
.del-line {
  color: rgba(0, 0, 0, 0.3);
  text-decoration: line-through;
}
.footer {
  display: flex;
  justify-content: space-around;
  height: 50px;
  padding: 10px 15px;
  color: #777;
  text-align: center;
  border-top: 1px solid #e6e6e6;
}
.footer .todo-count {
  float: left;
  line-height: 30px;
  text-align: left;
}
.footer .todo-count strong {
  font-weight: 300;
}
.footer .filters {
  display: flex;
  line-height: 30px;
  list-style: none;
}
.footer .filters li a {
  margin-right: 5px;
  padding: 3px 7px;
  color: inherit;
  text-decoration: none;
  border: 1px solid rgba(175, 47, 47, 0.2);
  border-radius: 3px;
}
.footer .clear-completed {
  position: relative;
  float: right;
  text-decoration: none;
  background: none;
  border: 0;
  cursor: pointer;
}
</style>
