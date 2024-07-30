<template>
  <div>
    <h1>{{ titulo }}</h1>
    <div class="filtro-container">
      <label>Filtro:</label>
      <input type="text" v-model="filtro" placeholder="Filter">
    </div>
    <table>
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>Email</th>
          <th>Address</th>
          <th>Phone</th>
          <th>Country</th>
          <th>City</th>
          <th></th>
        </tr>
        <tr>
          <th><input type="text" v-model="contactoNuevoObj.id"></th>
          <th><input type="text" v-model="contactoNuevoObj.name"></th>
          <th><input type="text" v-model="contactoNuevoObj.email"></th>
          <th><input type="text" v-model="contactoNuevoObj.address"></th>
          <th><input type="text" v-model="contactoNuevoObj.phone"></th>
          <th><input type="text" v-model="contactoNuevoObj.country"></th>
          <th><input type="text" v-model="contactoNuevoObj.city"></th>
          <th><button @click="guardaNuevo()">Nuevo</button></th>
        </tr>
        <tr v-if="indexParaEditar !== null">
          <th><input type="text" v-model="contactoEditarObj.id"></th>
          <th><input type="text" v-model="contactoEditarObj.name"></th>
          <th><input type="text" v-model="contactoEditarObj.email"></th>
          <th><input type="text" v-model="contactoEditarObj.address"></th>
          <th><input type="text" v-model="contactoEditarObj.phone"></th>
          <th><input type="text" v-model="contactoEditarObj.country"></th>
          <th><input type="text" v-model="contactoEditarObj.city"></th>
          <th><button @click="guardaEdicion()">Guardar</button></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(contacto, index) in contactosFiltrados" :key="contacto.id">
          <td>{{contacto.id}}</td>
          <td>{{contacto.name}}</td>
          <td>{{contacto.email}}</td>
          <td>{{contacto.address}}</td>
          <td>{{contacto.phone}}</td>
          <td>{{contacto.country}}</td>
          <td>{{contacto.city}}</td>
          <td>
            <button @click="eliminarContacto(index)">Eliminar</button>
            <button @click="EditarContacto(contacto, index)">Editar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'MiComponente',
  data() {
    return {
      titulo: 'Agenda de contactos',
      contactoNuevoObj: { 
        id: "", 
        name: "", 
        email: "", 
        address: "", 
        phone: "",
        country: "",
        city:""
      },
      contactoEditarObj: { 
        id: "", 
        name: "", 
        email: "", 
        address: "", 
        phone: "",
        country: "",
        city:""
      },  
      indexParaEditar: null, 
      filtro: '',
      contactos: [
        {id:1, name:"Alice Johnson", email:"Alice.johnson@example.com", address: "123 Maple Street", phone:"123-456-7890", country:"USA", city:"New York"},
        {id:2, name:"Bob Smith", email:"bob.smith@example.com", address: "456 Oak Avenue", phone:"987-654-3210", country:"Canada", city:"Toronto"},
        {id:3, name:"Carol White", email:"carol.white@example.com", address: "789 Pino Road", phone:"555-123-4567", country:"UK", city:"London"},
        {id:4, name:"David Brown", email:"david.brown@example.com", address: "321 Elm Street", phone:"444-555-6666", country:"Australia", city:"Sydney"},
        {id:5, name:"Emily Davis", email:"emily.davis@example.com", address: "645 Spruce Lane", phone:"333-444-5555", country:"USA", city:"Los Angeles"}
      ]
    }
  },
  computed: {
    contactosFiltrados() {
      return this.contactos.filter(contacto => {
        const filtroLower = this.filtro.toLowerCase();
        return contacto.name.toLowerCase().includes(filtroLower) || contacto.email.toLowerCase().includes(filtroLower);
      });
    }
  },
  methods: {
    guardaNuevo() {
      this.contactos.push(Object.assign({}, this.contactoNuevoObj));
      this.resetNuevoContacto();
    },
    eliminarContacto(index) {
      this.contactos.splice(index, 1);
    },
    guardaEdicion() {
      this.contactos[this.indexParaEditar] = Object.assign({}, this.contactoEditarObj);
      this.indexParaEditar = null;
    },
    EditarContacto(contacto, index) {
      this.indexParaEditar = index;
      this.contactoEditarObj = Object.assign({}, contacto);
    },
    resetNuevoContacto() {
      this.contactoNuevoObj = { 
        id: "", 
        name: "", 
        email: "", 
        address: "", 
        phone: "",
        country: "",
        city:""
      };
    }
  }
}
</script>

<style scoped>
h1 {
    color: #42b983;
}
.filtro-container {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
}
.filtro-container label {
    margin-right: 10px;
}
.filtro-container input[type="text"] {
    flex: 0 0 25%; /* Equivale a 3 de 12 columnas */
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #ddd;
    padding: 8px;
}
th {
    background-color: #f2f2f2;
    text-align: left;
}
input[type="text"] {
    width: 100%;
}
</style>