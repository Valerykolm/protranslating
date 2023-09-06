<template>
  <h1 class="text-center mt-3">List of clients</h1>
  <div class="container">
    <div class="row-auto justify-content-center">
      <div class="col-md-auto">
        <table class="table table-bordered caption-top">
            <caption>
              <div class="table_header">
                <p><b>Clients</b></p>
                <button>New client</button>
              </div>
              </caption>
        <thead v-if="clients.length > 0">
          <tr>
            <th scope="col">Name</th>
            <th scope="col">Email</th>
            <th scope="col">Phone</th>
            <th scope="col">Providers</th>
            <th scope="col"></th>
            <th scope="col"></th>
          </tr>
        </thead>
        <tbody>
          <tr 
            v-for="c in clients"
            :key="c.name"
          >
            <td>{{ c.name }}</td>
            <td>{{ c.email }}</td>
            <td>{{ c.phone }}</td>
            <td>{{ c.provider }}</td>
            <td><a href="#">Edit</a></td>
            <td>
              <button
                @click="handleDelete(c)"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
      </div>
    </div>
    <form action="#" class="m-5">
      <h4 class="mb-3">New client</h4>
      <div class="field">
        <label for="name">Name:</label>
        <input v-model="client" id="GET-name" type="text" name="name" />
      </div>
      <div class="field">
        <label for="email">Email:</label>
        <input v-model="email" id="GET-email" type="text" name="email" />
      </div>
      <div class="field">
        <label for="phone">Phone:</label>
        <input v-model="phone" id="GET-phone" type="text" name="phone" />
      </div>
      <div class="field">
        <label for="providers">Providers:</label>
        <input 
          v-model="provider"
          v-on:keydown.enter="add" 
          id="providers" 
          type="text" 
          name="providers" 
          class="width: 112px"
        />
        <button>Add Povider</button>
      </div>
      <div 
        class="field"
        v-for="p in providers"
        :key="p"
      >
        <input type="checkbox" name="1"/>
        <label for="1">Provider {{ p }}</label>
      </div>
      <button>Cancel</button>
      <button @click="add" type="button">Add Client</button>
    </form>
    <!--Edit client-->
    <!--<form action="#" class="m-5">
      <h4 class="mb-3">Edit client</h4>
      <div class="field">
        <label for="name">Name:</label>
        <input v-model="client" id="GET-name" type="text" name="name" />
      </div>
      <div class="field">
        <label for="email">Email:</label>
        <input v-model="email" id="GET-email" type="text" name="email" />
      </div>
      <div class="field">
        <label for="phone">Phone:</label>
        <input v-model="phone" id="GET-phone" type="text" name="phone" />
      </div>
      <div class="field">
        <label for="providers">Providers:</label>
        <input 
          v-model="provider"
          v-on:keydown.enter="add" 
          id="providers" 
          type="text" 
          name="providers" 
        />
        <button>Add Povider</button>
      </div>
      <div 
        class="field"
        v-for="p in providers"
        :key="p"
      >
        <input type="checkbox" name="1"/>
        <label for="1">Provider {{ p }}</label>
      </div>
      <button>Cancel</button>
      <button @click="add" type="button">Add Client</button>
    </form>-->
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      client: "default",
      clients: [
        {name: "Test", email: "test@krfs.com", phone: "305-555-0000", provider: "Provider1, Provider3, Provider5"},
        {name: "Test1", email: "test1@krfs.com", phone: "305-000-5555", provider: "Provider3"},
        {name: "Test2", email: "test2@krfs.com", phone: "305-333-0000", provider: "Provider2, Provider4"}
      ],
      email: "default",
      phone: "default",
      provider: "default",
      providers: ["1", "2", "3", "4", "5"],
    };
  },

  methods: {
    add() {
      const newClient = {
        name: this.client, 
        email: this.email, 
        phone: this.phone, 
        provider: this.provider,
      };

      this.clients.push(newClient);
      this.client = "";
      this.email = "";
      this.phone = "";
      this.provider = "";
    },
    
    handleDelete(clientToRemove) {
      this.clients = this.clients.filter(c => c !== clientToRemove);
    }
  }
};
</script>

<style src="./bootstrap.min.css"></style>
