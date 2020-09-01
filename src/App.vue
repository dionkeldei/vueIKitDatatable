<template>
  <div id="app">
    <table class="uk-table uk-table-striped">
    <thead>
        <tr>
            <th v-for="( header,i ) in tableHeaders" v-bind:key="i">{{header}}</th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="( data,i ) in currentData" v-bind:key="i">
            <td v-bind:id="data.id" v-for="( field,j ) in data.fields" v-bind:key="j">{{field}}</td>
        </tr>
    </tbody>
    </table>
    <p class="uk-text-center uk-text-meta">Página No. {{pageNum}}</p>
    <ul class="uk-pagination uk-flex-center" uk-margin>
    <li><a href="#" @click="pageNum -= 1"><span uk-pagination-previous></span></a></li>
    <li v-for="index in numOfPages" :key="index"><a href="#" @click="getPage(index)">{{index}}</a></li>
    <li><a href="#" @click="pageNum += 1"><span uk-pagination-next></span></a></li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      tableHeaders: [
        'Nombre'
      ],
      currentData: [],
      show: 2,
      showPageNum: true,
      numOfPages: 0,
      pageNum: 0,
      tableData: [
        {
        id: "5f4ea6e02e371febec0ee2aa",
        fields:{
          name: "Watkins Contreras"
        }
        },
        {
        id: "5f4ea6e0478874ee749c8d85",
        fields:{
          name: "Fitzpatrick Sweeney"
        }
        },
        {
        id: "5f4ea6e05846df317dac2275",
        fields:{
          name: "Lane Odonnell"
        }
        },
        {
        id: "5f4ea6e03886435fc6cad244",
        fields:{
          name: "Decker Hurst"
        }
        },
        {
        id: "5f4ea6e06b93cf50fac4a665",
        fields:{
          name: "Gomez Patton"
        }
        },
        {
        id: "5f4ea6e08aff80bb832e9644",
        fields:{
          name: "Heath Mitchell"
        }
        },
        {
        id: "5f4ea6e0467ecacabbf67f8a",
        fields:{
          name: "Jeanette Duffy"
        }
        },
        {
        id: "5f4ea6e02e371febec0ee2aa",
        fields:{
          name: "Watkins Contreras"
        }
        },
        {
        id: "5f4ea6e0478874ee749c8d85",
        fields:{
          name: "Fitzpatrick Sweeney"
        }
        },
        {
        id: "5f4ea6e05846df317dac2275",
        fields:{
          name: "Lane Odonnell"
        }
        },
        {
        id: "5f4ea6e03886435fc6cad244",
        fields:{
          name: "Decker Hurst"
        }
        },
        {
        id: "5f4ea6e06b93cf50fac4a665",
        fields:{
          name: "Gomez Patton"
        }
        },
        {
        id: "5f4ea6e08aff80bb832e9644",
        fields:{
          name: "Heath Mitchell"
        }
        },
        {
        id: "5f4ea6e0467ecacabbf67f8a",
        fields:{
          name: "Jeanette Duffy"
        }
        }
      ]
    }
  },
  methods: {
    initTable: function () {
      this.pageNum = 1
      this.numOfPages = this.tableData.length / this.show
      if(Math.floor(this.numOfPages) < this.numOfPages){
        this.numOfPages = Math.floor(this.numOfPages) + 1
      }
      this.countData()
    },
    countData: function () {
      this.currentData = []
      var startCount = (this.show * (this.pageNum - 1))
      var finishCount = startCount + this.show
      for(startCount; startCount < finishCount; startCount++){
        if(this.tableData[startCount] !== undefined){
          this.currentData.push(this.tableData[startCount])
        }
      }
    },
    getPage: function (page) {
      this.pageNum = page
    }
  },
  mounted () {
    this.initTable()
  },
  watch: {
    pageNum: function () {
      if(this.pageNum < 1){
        this.pageNum = 1
        return false
      }else if (this.pageNum > this.numOfPages){
        this.pageNum = this.numOfPages
        return false
      }
      this.countData()
    },
    show: function () {
      this.initTable()
    }
  },
  components: {
  }
}
</script>

<style>
</style>
