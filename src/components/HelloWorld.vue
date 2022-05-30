<template>
  <div>
    <form>
      <div class="">
        <label for="filterField">Field:</label>
          <select id="filterField" class="form-control" v-model="filterField" @change="onChange($event)">
            <option value="">Disable filters</option>
          <!--   <option value="isActive">Active user</option> -->
            <option value="name">Name</option>
            <option value="email">Email</option>
            <option value="balance">Balance</option>
            <option value="registered">Date registered</option>
          </select>
      </div>
      <div class="">
        <label for="filterQuery">Query:</label>
        <input type="text" id="filterQuery" class="form-control" v-model="filterQuery" :disabled="filterField.length===0">
      </div>
      <div class="">
        <label for="userStateActive">Active: Yes:</label>
        <input type="radio" v-bind:value="true" id="userStateActive" class="" v-model="filterUserState"
          selected>
        <label for="userStateInactive">No:</label>
        <input type="radio" v-bind:value="false" id="userStateInactive" class="" v-model="filterUserState">
      </div>
    </form>
    <div>
      <table class="table">
        <thead class="thead-dark">
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Active</th>
            <th scope="col">Balance</th>
            <th scope="col">Name</th>
            <th scope="col">Email</th>
         <!--   <th>Registered</th> -->
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id" v-show="filterRow(user)">
            <td>{{user.guid}}</td>
            <td>{{activeStatus(user)}}</td>
            <td>{{formatBalance(user.balance)}}</td>
            <td>{{user.name}}</td>
            <td>
              <a v-bind:href="'mailto:' + user.email">{{ user.email }}</a>
            </td>
         <!--   <td>{{formatDate(user.registered)}}</td> -->
          </tr>
        </tbody>
      </table> 
    </div>
  </div>
</template>

<script>


 // import axios from 'axios';

  export default {
    data() {
      return {
        filterField: '',
        filterQuery: '',
        filterUserState: false,
        currency: '€',
        users: [
          {
            "index": 0,
            "guid": "e526c8a9-fcca-4c63-92e9-55b9007e2294",
            "isActive": true,
            "balance": 1324.58,
            "name": "Myrna Haney",
            "email": "myrnahaney@bitrex.com",
            "registered": "201812-16T09:45:22"
          },
          {
            "index": 1,
            "guid": "0ce8fbd8-326d-45a4-a98c-201ed5e2d2b2",
            "isActive": false,
            "balance": 1076.42,
            "name": "Atkinson Wong",
            "email": "atkinsonwong@bitrex.com",
            "registered": "201607-10T07:20:34"
          },
          {
            "index": 2,
            "guid": "72fe3f2f-a2ff-4409-ae72-e2648563715c",
            "isActive": false,
            "balance": 1164.32,
            "name": "French Estes",
            "email": "frenchestes@bitrex.com",
            "registered": "202003-13T05:41:22"
          },
          {
            "index": 3,
            "guid": "f5f15646-38cb-469d-a029-297f55069bd0",
            "isActive": false,
            "balance": 2342.24,
            "name": "Cochran Delgado",
            "email": "cochrandelgado@bitrex.com",
            "registered": "201801-12T06:33:18"
          },
          {
            "index": 4,
            "guid": "176cc0b6-8a05-4926-a6a4-7970313cf81d",
            "isActive": true,
            "balance": 3418.33,
            "name": "Case Hewitt",
            "email": "casehewitt@bitrex.com",
            "registered": "201403-17T02:35:20"
          }
        ]
      };
    },
    mounted () {
     // axios
     //   .get('https://reqres.in/api/users?page=2')
     //   .then(response => (this.users = response.data.data))
    },
    methods: {
      filterRow(user) {
        return this.filterByUserState(user) && this.filterByQuery(user);
      },
      filterByQuery(user){
        let result = true;
        if (this.filterField.length > 0 && this.filterQuery.length > 0){
          let query = this.filterQuery.toLowerCase();
          let filterFieldValue = user[this.filterField].toString().toLowerCase();
          result = filterFieldValue.includes(query);
        }
        return result; 
      },
      filterByUserState(user){
        return this.filterUserState === user.isActive;
      },
      activeStatus(user) {
        return (user.isActive) ? 'Active' : 'Inactive';
      },
      formatBalance(balance) {
        return this.currency + balance.toFixed(2);
      },
      formatDate(date) {
        let registered = new Date(date);
        return registered.toLocaleString('en-US');
      },
      onChange(event) {
          if (event.target.value.length === 0){
            this.filterQuery = '';
          }
      }
    }
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
table{
  margin-left: 30vw;
  background-color: #b6aeae85;
  border-radius: 15px;
}
/* Table Header Color */
th {
    border-bottom: 1px solid;
}
/* Table Row Color */
tr{
  color:#2c3e50;
}
td{
  color: #201f1f;
}
/* Link Color */
a{
  color: #000fff;
}
/* Dropdown color */
select#filterField {
    background: #7fffd4;
}
/* Color Radio buttons when clicked */
th {
    border-bottom: 1px solid;
}
/* Color Radio buttons when clicked */
input[type="radio"]{
  accent-color:red;
}
/* color for Text field if disabled and disabled mouse cursor */ 
input:disabled {
  background-color:#545a5f;
  cursor: not-allowed;
}
</style>
