<template>
  <div>
    <form>
      <label for="filterField">
        Field:
        <select id="filterField" v-model="filterField">
          <option value="">Disable filters</option>
          <option value="isActive">Active user</option>
          <option value="name">Name</option>
          <option value="email">Email</option>
          <option value="balance">Balance</option>
          <option value="registered">Date registered</option>
        </select>
        {{ filterField }}
      </label>
      <label for="filterQuery">
        Query:
        <input type="text" id="filterQuery" v-model="filterQuery">
      </label>
      <span>
        Active:
        <label for="userStateActive">
          Yes:
          <input type="radio" v-bind:value="true" id="userStateActive" v-model="filterUserState"
          selected>
        </label>
        <label for="userStateInactive">
          No:
          <input type="radio" v-bind:value="false" id="userStateInactive" v-model="filterUserState">
        </label>
      </span>
    </form>
    <div>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Active</th>
            <th>Balance</th>
            <th>Name</th>
            <th>Email</th>
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
        console.log(user.name, ': ' , result);
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
a {
  color: #42b983;
}
</style>
