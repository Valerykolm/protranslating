<template>
  <transition name="new-client">
    <!--<div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
            <slot name="header">
              New client
            </slot>
          </div>

          <div class="modal-body">
            <slot name="body">
              default body
            </slot>
          </div>

          <div class="modal-footer">
            <slot name="footer">
              default footer
              <button class="modal-default-button" @click="$emit('close')">
                OK
              </button>
            </slot>
          </div>
        </div>
      </div>
    </div>-->
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <form action="#" class="m-5 p-5">
            <p><b>New client</b></p>
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
            <div class="field">
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
            <div 
              class="providers_block"
              v-for="p in providers"
              :key="p.name"
            >
              <input 
                type="checkbox"
                @click="addProvider(p.name)"    
                class="me-2"
              />
              <label>
                {{ p.name }} 
                <i class="icon-edit"></i>
                <i @click="handleDelete(p)" class="icon-trash"></i>
              </label>
            </div>
            <hr />
            <div class="new_form_button">
              <button class="me-2" @click="$emit('close')">Cancel</button>
              <button @click="add" type="button">Add Client</button>
            </div>
          </form>
        </div>
      </div> 
    </div>
  </transition>
</template>
<script>
export default {
  data() {
    return {
      showForm: false,
    }
  },

  methods: {
    
  }
}
</script>