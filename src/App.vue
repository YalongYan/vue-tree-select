<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div class="container">
      <Tree :data="treeData"/>
    </div>
  </div>
</template>

<script>
import Tree from './components/tree/Tree'

export default {
  name: 'App',
  data () {
    return {
      treeData: [
        {open: false, name: '1', level: 0, checked: true},
        // {open: false, name: '是是是', level: 0},
        {
          open: false,
          name: '2',
          level: 0,
          checked: false,
          children: [
            {
              open: false,
              name: '3',
              level: 1,
              checked: false,
              children: [
                {open: false, name: '4', level: 2, checked: false},
                {
                  open: false,
                  name: '5',
                  level: 2,
                  checked: false,
                  children: [
                    {
                      open: false,
                      name: '6',
                      level: 3,
                      checked: false,
                      children: [
                        {open: false, name: '7', level: 4, checked: false},
                        {open: false, name: '8', level: 4, checked: false}
                      ]
                    }
                  ]
                }
              ]
            },
            {open: false, name: '9', level: 1, checked: false},
            {open: false, name: '10', level: 1, checked: false},
            {
              open: false,
              name: '11',
              level: 1,
              checked: false,
              children: [
                {open: false, name: '12', level: 2, checked: false},
                {open: false, name: '13', level: 2, checked: false}
              ]
            }
          ]
        }
      ],
      // 选择表单的数据结果
      selectFormResult: []
    }
  },
  components: {
    Tree
  },
  methods: {
    calculateSelectFormResult: function () {
      // console.log(this.selectFormResult)
      var arr = []
      function f (obj) {
        for (var i in obj) {
          if (obj[i].checked) {
            // console.log(2)
            arr.push(obj[i].name)
          }
          if (obj[i].children) {
            // console.log(3)
            if (obj[i].children.length !== 0) {
              // console.log(4)
              f(obj[i].children)
            }
          }
        }
      }
      f(this.treeData)
      this.selectFormResult = arr
      console.log(this.selectFormResult)
    }
  },
  watch: {
    // 深度监听 treeDate的数据变化 用 deep
    treeData: {
      handler: function (newVal, oldVal) {
        this.calculateSelectFormResult()
      },
      deep: true
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
*{
  padding: 0;
  margin: 0;
}
.container{
  width: 600px;
  margin: 0 auto;
}
</style>
