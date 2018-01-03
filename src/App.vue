<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>GC Drinks CRUD</h1>
    </div>

  <div class="panel panel-default">
    <div class="panel-heading">
      <h3>Add a Person</h3>
    </div>
    <div class="panel-body">
      <form id="form" class="form-inline" v-on:submit.prevent="addPerson">
        <div class="form-group">
          <label for="bookTitle">Name: </label>
          <input type="text" id="bookTitle" class="form-control" v-model="newPerson.name">
        </div>
        <div class="form-group">
          <label for="bookAuthor">Tea: </label>
          <input type="text" id="bookAuthor" class="form-control" v-model="newPerson.tea">
        </div>
        <div class="form-group">
          <label for="bookUrl">Coffee: </label>
          <input type="text" id="bookUrl" class="form-control" v-model="newPerson.coffee">
        </div>
        <input type="submit" class="btn btn-primary" value="Add Person">
      </form>
    </div>
  </div>

    <div class="panel pannel-default">
      <div class="panel-heading">
        <h3>People List</h3>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>Name</th>
              <th>Tea</th>
              <th>Coffee</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="person in people" v-bind:key="person.id">
              <td>{{person.name}}</td>
              <td>{{person.tea}}</td>
              <td>{{person.coffee}}</td>
              <td><span class="glyphicon glyphicon-trash" v-on:click="deletePerson(person)"></span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import Firebase from "firebase";

let config = {
  apiKey: "AIzaSyCMtyxB1D9mlZP-Nw4w0o5pUYg5VgYa2NQ",
  authDomain: "gcdrinksapp.firebaseapp.com",
  databaseURL: "https://gcdrinksapp.firebaseio.com",
  projectId: "gcdrinksapp",
  storageBucket: "",
  messagingSenderId: "479063460151"
};

let app = Firebase.initializeApp(config);
let db = app.database();

let dbRef = db.ref("drinks");

export default {
  name: "app",
  firebase: {
    people: dbRef
  },
  data() {
    return {
      newPerson: {
        name: "",
        tea: "",
        coffee: ""
      }
    };
  },
  methods: {
    addPerson: function() {
      dbRef.push(this.newPerson);
      this.newPerson.name = "";
      this.newPerson.tea = "";
      this.newPerson.coffee = "";
    },
    deletePerson: function(person) {
      dbRef.child(person[".key"]).remove();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
