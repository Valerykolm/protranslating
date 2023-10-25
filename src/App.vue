<template>
  <h1 class="text-center mt-3">List of clients</h1>
  <div class="container">
    <div class="row-auto justify-content-center">
      <div class="col-md-auto">
        <table class="table table-bordered caption-top">
          <caption>
            <div class="table_header">
              <p>Clients</p>
              <button @click="showForm = true">New client</button>
              <!--<button @click="showModal = true">Показать модальное окно</button>
              <new-client v-if="showModal" @close="showModal = false">
              </new-client>-->
            </div>
          </caption>
          <thead v-if="clients.length > 0">
            <tr>
              <th scope="col">Name</th>
              <th scope="col">Email</th>
              <th scope="col">Phone</th>
              <th scope="col">Providers</th>
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
              <td>
                <a 
                  @click="selectedClient = c" 
                  href="#"
                >
                  Edit
                </a>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <!--New client-->
    <div v-if="showForm" class="form_mask">
      <div class="form_wrapper">
        <form class="form_container">
          <p class="form_header">New client</p>
          <hr />
          <div class="field">
            <label for="name">Name:</label>
            <input v-model="client" id="name" type="text" name="name" />
          </div>
          <div class="field">
            <label for="email">Email:</label>
            <input v-model="email" id="email" type="text" name="email" />
          </div>
          <div class="field">
            <label for="phone">Phone:</label>
            <input v-model="phone" id="phone" type="text" name="phone" />
          </div>
          <div class="field_providers">
            <label for="providers">Providers:</label>
            <input
              v-model="provider"
              @keydown.enter = "addNewProvider"
              id="providers" 
              type="text"  
            />
            <button @click="addNewProvider" type="button">Add Povider</button>
          </div>
          <div 
            class="providers_block"
          >
            <div
              v-for="p in providers"
              :key="p.name"
            >
              <input 
                type="checkbox"
                v-bind:value="p.name"
                v-model="checkedProvider"
                class="me-2"
              />
              <label>
                {{ p.name }} 
                <i class="icon-edit"></i>
                <i @click="handleDelete(p)" class="icon-trash"></i>
              </label>
            </div>
          </div>
          <hr />
          <div class="new_form_button">
            <button @click="showForm=false" class="me-2">Cancel</button>
            <button @click="add" type="button">Add Client</button>
          </div>
        </form>
      </div>
    </div>
    <!--Edit client-->
    <div v-if="selectedClient" class="form_mask">
      <div class="form_wrapper">
        <form  action="#" class="form_container">
          <p class="form_header">Edit client</p>
          <hr />
          {{ selectedClient }}
          <div class="field">
            <label for="name">Name:</label>
            <input v-model="selectedClient.name" id="name" type="text" name="name" />
          </div>
          <div class="field">
            <label for="email">Email:</label>
            <input v-model="selectedClient.email" id="email" type="text" name="email" />
          </div>
          <div class="field">
            <label for="phone">Phone:</label>
            <input v-model="selectedClient.phone" id="phone" type="text" name="phone" />
          </div>
          <div class="field_providers">
            <label for="providers">Providers:</label>
            <input
              v-model="provider"
              @keydown.enter = "addNewProvider"
              id="providers" 
              type="text"  
              class="provider_input"
            />
            <button @click="addNewProvider" type="button">Add Povider</button>
          </div>
          <div class="providers_block">
            
            <div 
              v-for="p in providers"
              :key="p.name"
            >
              <input 
                type="checkbox"
                v-bind:value="p.name"    
                v-model="selectedClient.providerToAdd"
                class="me-2"
              />
              <label>
                {{ p.name }} 
                <i class="icon-edit"></i>
                <i @click="handleDelete(p)" class="icon-trash"></i>
              </label>
            </div>
          </div>
          <hr />
          <div class="new_form_button">
            <button @click="deleteClient(selectedClient)" class="me-4 delete">Delete Client</button>
            <button @click="selectedClient = null" class="me-2">Cancel</button>
            <button @click="selectedClient = null">Save Client</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "App",

  data() {
    return {
      client: "",
      email: "",
      phone: "",
      provider: "",
      id: 5,
      showForm: false,
      checked: false,

      selectedClient: null,

      // selectedClient: {
      //   name: this.client.name,
      //   email: this.client.email,
      //   phone: this.client.phone,
      //   provider: this.client.provider,
      // },

      clients: [
        {name: "Test", email: "test@krfs.com", phone: "305-555-0000", provider: "Provider1, Provider2, Provider3"},
        {name: "Test1", email: "test1@krfs.com", phone: "305-000-5555", provider: "Provider3"},
        {name: "Test2", email: "test2@krfs.com", phone: "305-333-0000", provider: "Provider2, Provider4"}
      ],
      providers: [
        {id: 1, name: "Provider1"}, 
        {id: 2, name: "Provider2"},
        {id: 3, name: "Provider3"},
        {id: 4, name: "Provider4"},
        {id: 5, name: "Provider5"},
      ],
      checkedProvider: [],
      checkedEditProvider: [],
    };
  },

  // watch: {
  //   selectedClient() {
  //     this.checkedEditProvider = [];
  //     this.checkedProvider.map((p) => this.checkedEditProvider.push(p));
  //     this.checkedProvider = [];
  //   }
  // },

  methods: {
    add() {
      const newClient = {
        name: this.client, 
        email: this.email, 
        phone: this.phone, 
        provider: this.checkedProvider.join(', '),
        providerToAdd: this.checkedProvider,
      };

      this.clients.push(newClient);
      this.client = "";
      this.email = "";
      this.phone = "";
      this.provider = "";

      this.showForm = false;
      this.checkedProvider = [];
    },

    // addProvider(p) {
    //   this.checkedProvider.push(p); 
    //   this.provider = "";
    // },

    addNewProvider() {
      const newProvider = {
        id: this.id + 1,
        name: this.provider,
      }

      this.providers.push(newProvider);
      this.provider = "";
    },

    // showProvider() {
    //   this.checkedProvider?.name;
    // },

    handleDelete(providerToRemove) {
      this.providers = this.providers.filter(p => p !== providerToRemove);
    },

    deleteClient(clientToRemove) {
      this.clients = this.clients.filter(c => c !== clientToRemove);
      this.selectedClient = null;
    },
  }
};
</script>
<style src="./assets/bootstrap.min.css"></style>
<style src="./assets/fontello.css"></style>
