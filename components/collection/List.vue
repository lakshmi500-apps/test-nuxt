<template>
    <button @click="addContacts">Add Contacts</button>
    <ul
      role="list"
      class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3 p-5 mt-[100px] bg-black"
    >
      <li
        v-for="(person, index) in contacts"
        :key="index"
        class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow"
      >
        <div class="flex w-full items-center justify-between space-x-6 p-6">
          <div class="flex-1 truncate">
            <div class="flex items-center space-x-3">
              <h3 class="truncate text-sm font-medium text-gray-900">
                Name : {{ person.name }}
              </h3>
              <span
                class="inline-block flex-shrink-0 rounded-full bg-green-100 px-2 py-0.5 text-xs font-medium text-green-800"
                >Phone : {{ person.phone }}</span
              >
            </div>
            <p class="mt-1 truncate text-sm text-gray-500">
              Country : {{ person.country }}
            </p>
          
          </div>
          <img
            class="h-10 w-10 flex-shrink-0 rounded-full bg-gray-300"
            src="https://creazilla-store.fra1.digitaloceanspaces.com/cliparts/7803/girl-taking-a-test-clipart-xl.png"
            alt=""
          />
        </div>
        <div>
          <div class="-mt-px flex divide-x divide-gray-200">
            <div class="flex w-0 flex-1">
             
            </div>
          </div>
        </div>
        <button @click="editContact(person, index)">Edit</button>
        <br />
        <button @click="deleteContact(person, index)">Delete</button>
      </li>
    </ul>
  </template>
  
  <script setup lang="ts">
  
  import { Vue2 } from "nuxt/dist/app/compat/vue-demi";
  import { ref } from "vue";
  
  const people = [

    // More people...
  ];
  const props = defineProps({
    contacts: {
      type: Array,
    },
  });
  // Declaring Emits
  const emit = defineEmits([
    "addContact",
    "editContact",
    "deleteContact",
  ]);
  
  const addContacts = () => {
    emit("addContact");
  };
  
  const editContact = (person: any, index: any) => {
    emit("editContact", person, index);
  };
  const deleteContact = (person: any, index: any) => {
    emit("deleteContact", person, index);
  };
  </script>
  