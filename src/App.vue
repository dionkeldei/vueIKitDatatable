<template>
  <div id="app">
    <table v-if="!selectable" class="uk-table uk-table-striped uk-table-hover">
    <thead>
        <tr>
            <th v-for="( header,i ) in headers" v-bind:key="i">{{header}}</th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="( data,i ) in currentData" v-bind:key="i" :class="isLink(i)" @click="goTo(i)">
            <td v-bind:id="data.id" v-for="( field,j ) in data.fields" v-bind:key="j">{{field}}</td>
        </tr>
    </tbody>
    </table>

    <table v-if="selectable" class="uk-table uk-table-striped uk-table-hover">
    <thead>
        <tr>
            <th v-for="( header,i ) in headers" v-bind:key="i">{{header}}</th>
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
  props: {
    headers: Array,
    fields: Array,
    show: Number,
    search: String,
    selectable: Boolean,
    selected: Array
  },
  data () {
    return {
      currentData: [],
      showPageNum: true,
      numOfPages: 0,
      pageNum: 0,
      selectedid: [],
      checked: [],
      checkVisibility: [
        false,
        true
      ],
      /*selectable: false,
      headers: [
        'Nombre',
        'Mail'
      ],
      show: 6,
      search: '',
      fields: [
        {
        id: "1",
        fields:[
          "Watkins Contreras",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "2",
        link: "https://facebook.com",
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
        link: "https://google.com",
        fields:[
          "Decker Hurst",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "5",
        link: "https://google.com",
        fields:[
          "Gomez Patton",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "6",
        link: "https://google.com",
        fields:[
          "Heath Mitchell",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "7",
        link: "https://google.com",
        fields:[
          "Jeanette Duffy",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "8",
        link: "https://google.com",
        fields:[
          "Watkins Contreras",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "9",
        link: "https://google.com",
        fields:[
          "Fitzpatrick Sweeney",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "10",
        link: "https://google.com",
        fields:[
          "Lane Odonnell",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "11",
        link: "https://google.com",
        fields:[
          "Decker Hurst",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "12",
        link: "https://google.com",
        fields:[
          "Gomez Patton",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "13",
        link: "https://google.com",
        fields:[
          "Heath Mitchell",
          "hhh@ghbd.com"
        ]
        },
        {
        id: "14",
        link: "https://google.com",
        fields:[
          "Jeanette Duffy",
          "hhh@ghbd.com"
        ]
        }
      ],*/
      data: []
    }
  },
  methods: {
    initTable: function () {
      if(this.fields.length <= 0){
        return false
      }
      this.pageNum = 1
      this.numOfPages = this.data.length / this.show
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
        if(this.data[startCount] !== undefined){
          this.currentData.push(this.data[startCount])
        }
      }
    },
    selectRow: function (id) {
      if(!this.selectedid.includes(id)){
        this.selectedid.push(id)
      }else{
        var selected = this.selectedid
        this.selectedid = []
        for(var i = 0;i < selected.length; i ++){
          if(selected[i] !== id)
          this.selectedid.push(selected[i])
        }
      }
      this.$emit('selectupdate', this.selectedid)
    },
    getPage: function (page) {
      this.pageNum = page
    },
    getChecked: function () {
      this.checked = []
      for(var i = 0; i < this.data.length; i++){
        if(this.selectedid.includes(this.data[i].id)){
          this.checked[this.data[i].id] = true
        }else{
          this.checked[this.data[i].id] = false
        }
      }
    },
    isLink: function (i) {
      if(this.currentData[i].link){
        return 'link-ff-table-683669635693'
      }
    },
    goTo: function (i) {
      if(this.currentData[i].link){
        window.location.href = this.currentData[i].link;
      }
    }
  },
  mounted () {
    this.data = this.fields
    if(this.selected !== undefined){
       this.selectedid = this.selected
    }
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
    selectedid: function () {
      this.getChecked()
    },
    search: function () {
      var str = this.search.toLowerCase()
      if(str === ''){
        this.data = this.fields
        this.initTable()
        return false
      }
      this.data = []
      for(var i = 0; i < this.fields.length; i++){
        var hasIt = false
        for(var j = 0; j < this.fields[i].fields.length; j++){
          var checkStr = this.fields[i].fields[j].toLowerCase()
          if(checkStr.includes(str)){
            hasIt = true
          }
        }
        if(hasIt === true){
          this.data.push(this.fields[i])
        }
      }
      this.initTable()
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
