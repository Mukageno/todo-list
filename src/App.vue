<template>
  <div class="todolist">
    <h1>To Do List</h1>
    <div class="todolist-addtask">
      <input type="text" id="task" v-model="value" />
      <span id="add-task" @click="addTask()"
        ><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
          <path
            fill="#ccc"
            d="M256 512c141.4 0 256-114.6 256-256S397.4 0 256 0S0 114.6 0 256S114.6 512 256 512zM232 344V280H168c-13.3 0-24-10.7-24-24s10.7-24 24-24h64V168c0-13.3 10.7-24 24-24s24 10.7 24 24v64h64c13.3 0 24 10.7 24 24s-10.7 24-24 24H280v64c0 13.3-10.7 24-24 24s-24-10.7-24-24z"
          /></svg
      ></span>
    </div>
    <ul>
      <li v-for="(item, idx) in list" :key="item.idx">
        <label>
          <input type="checkbox" v-model="list[idx].isVariable" />
          <span> {{ idx + 1 }}{{ item.text }}</span>
        </label>
        <button type="button" class="del-btn" @click="removeTask(idx)">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
            <!--! Font Awesome Pro 6.3.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
            <path
              d="M135.2 17.7C140.6 6.8 151.7 0 163.8 0H284.2c12.1 0 23.2 6.8 28.6 17.7L320 32h96c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 96 0 81.7 0 64S14.3 32 32 32h96l7.2-14.3zM32 128H416V448c0 35.3-28.7 64-64 64H96c-35.3 0-64-28.7-64-64V128zm96 64c-8.8 0-16 7.2-16 16V432c0 8.8 7.2 16 16 16s16-7.2 16-16V208c0-8.8-7.2-16-16-16zm96 0c-8.8 0-16 7.2-16 16V432c0 8.8 7.2 16 16 16s16-7.2 16-16V208c0-8.8-7.2-16-16-16zm96 0c-8.8 0-16 7.2-16 16V432c0 8.8 7.2 16 16 16s16-7.2 16-16V208c0-8.8-7.2-16-16-16z"
            />
          </svg>
        </button>
      </li>
    </ul>
    <div class="todolist-btns">
      <button type="button" @click="removeCompleted(list)">
        Clear Completed
      </button>
      <button type="button" @click="clearAll()">Clead All</button>
    </div>
  </div>
</template>
 
<script>
export default {
  data() {
    return {
      value: null,
      list: [],
    };
  },
  methods: {
    addTask() {
      if (
        this.value.length >= 1 &&
        this.value != null &&
        typeof this.value !== "undefined"
      ) {
        this.list.push({
          text: this.value,
          isVariable: false,
        });
        this.value = "";
      }
      console.log(this.list);
    },
    addTaskByEnter() {
      document.addEventListener("keyup", (event) => {
        if (event.code === "Enter" || event.keyCode === 13) {
          if (
            this.value.length >= 1 &&
            this.value != null &&
            typeof this.value !== undefined
          ) {
            this.list.push({
              text: this.value,
              isVariable: false,
            });
            this.value = "";
          }
        }
      });
    },
    removeTask(idx) {
      console.log(this.list);
      for (const i in this.list) {
        this.list.slice(idx, 1);
      }
    },
    clearAll() {
      this.list = [];
    },
    removeCompleted(list) {
      for (const i in list) {
        console.log(this.list[i].isVariable);
        if (this.list[i].isVariable === true) {
          console.log(this.list);
        }
      }
    },
  },
  created() {
    this.addTaskByEnter();
  },
  components: {},
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  font-family: Arial;
}
body {
  background: #00ccff;
}
.todolist {
  background: #fff;
  max-width: 700px;
  min-height: 500px;
  width: 100%;
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.5);
  border-radius: 20px;
  padding: 20px;
  margin: 100px auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  &-addtask {
    width: 100%;
    display: flex;
    align-items: center;
    border: 1px solid #000;
    border-radius: 10px;
    padding: 0 5px;
    input {
      width: 100%;
      height: 40px;
      border: none;
      outline: none;
      font-size: 20px;
    }
    span {
      padding: 0 5px;
      cursor: pointer;
      svg {
        width: 30px;

        path {
          transition: 0.3s linear;
          &:hover {
            fill: #000;
          }
        }
      }
    }
  }
  &-btns {
    margin-top: auto;
    display: flex;
    gap: 20px;
    button {
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
      border: none;
      outline: none;
      background: transparent;
      border: 1px solid #000;
    }
  }
  ul {
    padding: 15px 20px;
    list-style: none;
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 10px;
    li {
      line-height: 25px;
      display: flex;
      align-items: center;
      transition: 0.2s;
      padding: 0 10px;
      border-radius: 5px;
      &:hover {
        background: rgba(0, 0, 0, 0.1);
      }
      label {
        width: 100%;
        display: flex;
        align-items: center;
        gap: 10px;
        padding: 10px 0;

        cursor: pointer;
        input:checked + span {
          position: relative;
          &::before {
            width: 100%;
          }
        }
        span {
          word-break: break-all;
          position: relative;
          &::before {
            content: "";
            position: absolute;
            top: 50%;
            left: 0;
            width: 0;
            transition: 0.1s;
            transform: translateY(-50%);
            height: 1px;
            background: #000;
          }
        }
      }
      button {
        background: transparent;
        border: none;
        cursor: pointer;
        svg {
          width: 20px;

          path {
            fill: #ccc;
            transition: 0.3s;
          }
          &:hover {
            path {
              fill: #000;
            }
          }
        }
      }
    }
  }
  @keyframes checked {
    0% {
      width: 0;
    }
    100% {
      width: 100%;
    }
  }
}
</style>
