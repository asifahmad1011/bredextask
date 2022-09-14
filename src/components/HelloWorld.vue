<template>
  <div class="hello">

    <button @click="fetchData()">Fetch Data From API</button>

    <table class="table table-striped table-hover">
      <thead v-if="api_data.data">
        <tr>
          <!-- <th>id</th> -->
          <th>Name</th>
          <th>Address</th>
          <th>Email</th>
          <th>Company</th>
          <th>Phone #</th>
          <th>Website</th>
          <!-- <th>Allignment</th> -->
        </tr>
      </thead>
      <tbody>
        <tr v-for="(person, index) in api_data.data" :key="index">
          <!-- <td>{{ person.id }}</td> -->
          <td>{{ person.name }}</td>
          <td>{{ person.address.city }}</td>
          <td>{{ person.email }}</td>
          <td>{{ person.company.name }}</td>
          <td>{{ person.phone }}</td>
          <td>{{ person.website }}</td>
        </tr>
      </tbody>
    </table>

  <br />

    <button @click="postUser()">Register User</button>

  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      api_data: []
    }
  },

  methods: {
    fetchData: async function () {
      let headers = {
        'accept': 'application/json',
        // please add bearer token here
        'Authorization': 'Bearer *********'
      }
      this.api_data = await axios.get(
        'https://zeigsuns.bredex.de', { headers }

      )
      // .then(response => (this.api_data = response))

      console.log(this.api_data)
    },

    postUser: async function () {
      let testUser =
      {
        name: "Janice Romero",
        username: "Janice123",
        email: "janice.romero@example.com",
        address: {
          street: "Lindentwete 1",
          suite: "Suite B",
          city: "Braunschweig",
          zipcode: "38100",
          geo: {
            lat: "52.2648197",
            lng: "10.5180167"
          }
        },
        phone: "+49 123 4567890",
        website: "https://example.com",
        company: {
          name: "BREDEX GmbH",
          catchPhrase: "Gemeinsam gestalten wir Ihren digitalen Wandel",
          bs: "Maßgeschneiderte Software-Lösungen"
        }
      }
      let headers = {
        'accept': 'application/json',
        'Authorization': 'Bearer OxBONbQaVU6zYG3G0QeN',
        'Content-Type': 'application/json'
      }

      this.api_data = await axios.post(
        'https://zeigsuns.bredex.de', { headers, testUser }

      ).then(function (response) {
        console.log(response);
      })
        .catch(function (error) {
          console.log(error);
        });
    }


  }






}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

table {
  font-family: "Open Sans", sans-serif;
  width: 1000px;
  border-collapse: collapse;
  border: 3px solid #44475c;
  margin: 10px 10px 0 10px;
}

table th {
  text-transform: uppercase;
  text-align: left;
  background: #44475c;
  color: #fff;
  padding: 8px;
  min-width: 30px;
}

table td {
  text-align: left;
  padding: 8px;
  border-right: 2px solid #7d82a8;
}

table td:last-child {
  border-right: none;
}

table tbody tr:nth-child(2n) td {
  background: #d4d8f9;
}
</style>
