<template>
  <div id="app">
    <div class="add">
      编号:<input type="text" v-model="subject.id"/>
      品牌名称:<input type="text" v-model="subject.name"/>
      <input type="button" value="添加" @click="add"/>
    </div>
    <div class="add">
      品牌名称:
      <input type="text" placeholder="请输入搜索条件" />
    </div>
    <div>
      <table class="tb">
        <tr>
            <th>编号</th>
            <th>品牌名称</th>
            <th>创立时间</th>
            <th>操作</th>
        </tr>
        <tr v-for="(value,index) in list" :key='index'>
            <td>{{value.id}}</td>
            <td>{{value.name}}</td>
            <td>{{value.time|dateFormat}}</td>
            <td>
                <a href="#" @click="del(index)">删除</a>
            </td>
        </tr>
        <tr>
          <td colspan="4" v-show="list.length==0">没有数据了</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list: [
        { id: 1, name: 'java', time: new Date() },
        { id: 2, name: 'UI', time: new Date() },
        { id: 3, name: 'python', time: new Date() }
      ],

      subject: {
        id: '',
        name: '',
        time: new Date()
      }
    }
  },

  methods: {
    add () {
      this.list.push({ ...this.subject })
    },
    del (index) {
      this.list.splice(index, 1)
    }
  },
  filters: {
    dateFormat (time) {
      let year = time.getFullYear()
      let month = time.getMonth() + 1
      let day = time.getDate()
      return `${year}-${month}-${day}`
    }

  }
}
</script>

<style lang='less' scoped>
#app {
  width: 600px;
  margin: 10px auto;
}

.tb {
  border-collapse: collapse;
  width: 100%;
}

.tb th {
  background-color: #0094ff;
  color: white;
}

.tb td,
.tb th {
  padding: 5px;
  border: 1px solid black;
  text-align: center;
}

.add {
  padding: 5px;
  border: 1px solid black;
  margin-bottom: 10px;
}
</style>
