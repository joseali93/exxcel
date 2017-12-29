<template>
  <div id="app">
   {{json_data}}
   <button @click="excel()">
     excel
   </button>
<!--
   <download-excel
      class   = "btn btn-default"
      :data   = "estados"
      :fields = "json_fields"
      name    = "filename.xls">
     
    </download-excel>
    -->
  </div>
</template>

<script>
import JsonExcel from 'vue-json-excel';

export default {
  methods:{
    excel(){
      console.log("entro a descagar excel");
              alasql('SELECT name as NOMBRE,'+
              'city as CIUDAD,'+
              'detalles->nombre as NOMBRE_DETALLE,'+
                            'detalles->servicio->id as ID_SERVICIO,'+
              'detalles->servicio->nombreser as NOMBRE_SERVICIO'+
              ' INTO XLS("Data.xls",{headers:true}) FROM ?',[this.json_data]);

    }
  },
  components:{
    downloadExcel: JsonExcel
  },
  name: 'app',
  data () {
    return {
      estados:{},
      msg: 'Welcome to Your Vue.js App',
      json_fields : {
            "_id"      : "Id Mongo",
            "id"      : "id",
            "nombre"   : "Nombre",

        },
        titulos: {},
    json_data : [
            {
                name      : "Tony Peña",
                city      : "New York",
                country  : "United States",
                birthdate : "1978-03-15",
                amount    : 42,
                detalles: {
                    nombre: 'pepe',
                    servicio: {
                        id: '123123',
                        nombreser: 'aaaaaaaaaaa'
                    }

                }
            },
            {
                name      : "Tony penañscos",
                city      : "New York",
                country  : "United States",
                birthdate : "1978-03-15",
                amount    : 42,
                detalles: {
                    nombre: 'pepe',
                    servicio: {
                        id: '44444',
                        nombreser: 'alslasa'
                    }

                }
            }
        ],
        
    }
  },
  mounted: function(){

      for (var key in this.json_data) {
        console.log(key);
        console.log(Object.keys(this.json_data[key]));
        this.titulos=Object.keys(this.json_data[key])
      }
  }
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
</style>
