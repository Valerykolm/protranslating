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
              <td>{{ convertedToString(c) }}</td>
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
            <input v-model="client" @keydown.enter="add" id="name" type="text" name="name" />
          </div>
          <div class="field">
            <label for="email">Email:</label>
            <input v-model="email" @keydown.enter="add" id="email" type="text" name="email" />
          </div>
          <div class="field">
            <label for="phone">Phone:</label>
            <input v-model="phone" @keydown.enter="add" id="phone" type="text" name="phone" />
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
              :key="p.id"
            >
              <input 
                type="checkbox"
                v-bind:value="p.id"
                v-model="checkedProvider"
                class="me-2"
                :id="p.id"
              />
              <label :for="p.id">
                {{ p.name }} 
                <i class="icon-edit"></i>
                <i @click="handleDelete(p)" class="icon-trash"></i>
              </label>
            </div>
          </div>
          <hr />
          <div class="add_buttons">
            <button @click="cleanForm" class="me-2">Cancel</button>
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
          <div class="field">
            <label for="name">Name:</label>
            <input v-model="selectedClient.name" @keydown.enter="save" id="name" type="text" name="name" />
          </div>
          <div class="field">
            <label for="email">Email:</label>
            <input v-model="selectedClient.email" @keydown.enter="save" id="email" type="text" name="email" />
          </div>
          <div class="field">
            <label for="phone">Phone:</label>
            <input v-model="selectedClient.phone" @keydown.enter="save" id="phone" type="text" name="phone" />
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
              :key="p.id"
            >
              <input 
                type="checkbox"
                v-bind:value="p.id"    
                v-model="selectedClient.providerToAdd"
                class="me-2"
                :id="p.id"
              />
              <label :for="p.id">
                {{ p.name }} 
                <i class="icon-edit"></i>
                <i @click="handleDelete(p)" class="icon-trash"></i>
              </label>
            </div>
          </div>
          <hr />
          <div class="new_form_button">
            <button @click="deleteClient(selectedClient)" class="me-4 delete">Delete Client</button>
            <div>
              <button @click="cancelToEdit" class="me-2">Cancel</button>
              <button @click="save">Save Client</button>
            </div>
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
      provider: [],
      checkedProvider: [],

      id: 5,
      showForm: false,

      selectedClient: null,

      clients: [
        {name: "Test", nameToAdd: "Test", email: "test@krfs.com", emailToAdd: "test@krfs.com", phone: "305-555-0000", phoneToAdd: "305-555-0000", provider: [1, 3, 5], providerToAdd: [1, 3, 5]},
        {name: "Test1", nameToAdd: "Test1", email: "test1@krfs.com", emailToAdd: "test1@krfs.com", phone: "305-000-5555", phoneToAdd: "305-000-5555", provider: [3], providerToAdd: [3]},
        {name: "Test2", nameToAdd: "Test2", email: "test2@krfs.com", emailToAdd: "test2@krfs.com", phone: "305-333-0000", phoneToAdd: "305-333-0000", provider: [2, 4], providerToAdd: [2, 4]}
      ],
      providers: [
        {id: 1, name: "Provider1"}, 
        {id: 2, name: "Provider2"},
        {id: 3, name: "Provider3"},
        {id: 4, name: "Provider4"},
        {id: 5, name: "Provider5"},
      ],
    };
  },

  methods: {
    add() {
     const newClient = {
        name: this.client,
        nameToAdd: this.client, 
        email: this.email,
        emailToAdd: this.email, 
        phone: this.phone,
        phoneToAdd: this.phone, 
        provider: this.checkedProvider,
        providerToAdd: this.checkedProvider,
      };

      this.clients.push(newClient);

      this.cleanForm();
    },

    save() {
      this.selectedClient.provider = this.selectedClient.providerToAdd;
      this.selectedClient.nameToAdd = this.selectedClient.name;
      this.selectedClient.emailToAdd = this.selectedClient.email;
      this.selectedClient.phoneToAdd = this.selectedClient.phone;

      this.selectedClient = null;
    },

    addNewProvider() {
      const newProvider = {
        id: this.id + 1,
        name: this.provider,
      }

      this.providers.push(newProvider);
      this.provider = [];
    },

    handleDelete(providerToRemove) {
      this.providers = this.providers.filter(p => p !== providerToRemove);
    },

    deleteClient(clientToRemove) {
      this.clients = this.clients.filter(c => c !== clientToRemove);
      this.selectedClient = null;
    },

    convertedToString(client) {
      const currentProvider = client.provider.map((idProvider) => this.providers.filter(p => p.id === idProvider)[0]?.name);
      return currentProvider.join(', ');
    },

    cancelToEdit() {
      this.selectedClient.name = this.selectedClient.nameToAdd;
      this.selectedClient.email = this.selectedClient.emailToAdd;
      this.selectedClient.phone = this.selectedClient.phoneToAdd;
      this.selectedClient.providerToAdd = this.selectedClient.provider;

      this.selectedClient = null;
    },

    cleanForm() {
      this.client = "";
      this.email = "";
      this.phone = "";
      this.provider = [];

      this.showForm = false;
      this.checkedProvider = [];
    },
  }
};
</script>
<style src="./assets/bootstrap.min.css"></style>
<style src="./assets/fontello.css"></style>
