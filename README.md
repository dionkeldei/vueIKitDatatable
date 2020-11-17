# datatable

## Ejemplo
```
<link rel="stylesheet" href="./vueDataTable.css">

<div id="app-assign">
  <data-table :headers="headers" :search="search" :fields="fields" :selectable="selectable" :show="show"/>
</div>

<script src="./vueDataTable.umd.min.js"></script>
<script>
new Vue({
  name: 'ibizaDataTable',
  data: {
    fields: [
    id: 1,
    fields: [
    'curso1',
    'Estado1',
    'Pago1',
    'Descarga1'
    ]
    ],
    headers: ['Curso', 'Estado','Pago','Descarga'],
    show: 6,
    selectable: false,
    search: ''
  },
  components: {
    dataTable: vueDataTable
  }
}).$mount('#app-assign')
</script>
```
## Ejemplo Fields
```
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
        link: "https://facbkk.com",
        fields:[
          "Fitzpatrick Sweeney",
          "hhh@ghbd.com"
        ]
        }]
```
## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
