<template>
  <div id="app">
    <table v-if="!selectable" class="uk-table uk-table-striped">
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

    <table v-if="selectable" class="uk-table uk-table-striped uk-table-hover">
    <thead>
        <tr>
            <th v-for="( header,i ) in tableHeaders" v-bind:key="i">{{header}}</th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="( data,i ) in currentData" v-bind:key="i"  @click="selectRow(data.id)" class="link-ff-table-683669635693">
            <td v-bind:id="data.id" v-for="( field,j ) in data.fields" v-bind:key="j">
              <span v-if="checked[data.id] && j === 0" uk-icon="icon: check; ratio: 1.4" class="uk-text-primary"></span>
              {{field}}
            </td>
        </tr>
    </tbody>
    </table>

    <p v-if="showPageNum" class="uk-text-center uk-text-meta">Página No. {{pageNum}}</p>
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
        'Nombre',
        'Mail'
      ],
      currentData: [],
      show: 6,
      showPageNum: true,
      numOfPages: 0,
      pageNum: 0,
      checked: [],
      selectable: true,
      checkVisibility: [
        false,
        true
      ],
      selectedRows: [
        '1',
        '2',
        '3',
        '7'
      ],
      tableData: [
        {
        id: "1",
        fields:[
          "Watkins Contreras",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "2",
        fields:[
          "Fitzpatrick Sweeney",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "3",
        fields:[
          "Lane Odonnell",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "4",
        fields:[
          "Decker Hurst",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "5",
        fields:[
          "Gomez Patton",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "6",
        fields:[
          "Heath Mitchell",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "7",
        fields:[
          "Jeanette Duffy",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "8",
        fields:[
          "Watkins Contreras",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "9",
        fields:[
          "Fitzpatrick Sweeney",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "10",
        fields:[
          "Lane Odonnell",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "11",
        fields:[
          "Decker Hurst",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "12",
        fields:[
          "Gomez Patton",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "13",
        fields:[
          "Heath Mitchell",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "14",
        fields:[
          "Jeanette Duffy",
          "hhh@ghbd.com"
        ]
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
      this.getChecked()
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
    selectRow: function (id) {
      if(!this.selectedRows.includes(id)){
        this.selectedRows.push(id)
      }else{
        var selected = this.selectedRows
        this.selectedRows = []
        for(var i = 0;i < selected.length; i ++){
          if(selected[i] !== id)
          this.selectedRows.push(selected[i])
        }
      }

    },
    getPage: function (page) {
      this.pageNum = page
    },
    getChecked: function () {
      this.checked = []
      for(var i = 0; i < this.tableData.length; i++){
        if(this.selectedRows.includes(this.tableData[i].id)){
          this.checked[this.tableData[i].id] = true
        }else{
          this.checked[this.tableData[i].id] = false
        }
      }
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
    },
    selectedRows: function () {
      this.getChecked()
    }
  },
  components: {
  }
}
</script>

<style>
  .link-ff-table-683669635693{
    cursor: pointer;
  }
</style>
