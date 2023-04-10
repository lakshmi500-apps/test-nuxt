<template>
  <div class="border-b border-gray-200 bg-white px-4 py-5 sm:px-6">
    <div class="-ml-4 -mt-2 flex flex-wrap items-center justify-between sm:flex-nowrap">
      <div class="ml-4 mt-2">
        <div class="flex">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="M9 8.25H7.5a2.25 2.25 0 00-2.25 2.25v9a2.25 2.25 0 002.25 2.25h9a2.25 2.25 0 002.25-2.25v-9a2.25 2.25 0 00-2.25-2.25H15m0-3l-3-3m0 0l-3 3m3-3V15" />
</svg>
        <h3 class="text-base font-semibold leading-6 text-gray-900">Vue</h3>
      </div>
      </div>
      <div class="ml-4 mt-2 flex-shrink-0">
        <button type="button" class="relative inline-flex items-right rounded-md bg-indigo-600 px-9 py-2 text-sm font-semibold
         text-white shadow-sm focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 
        ">Login Name: Lakshmi </button>
          
      </div>
    </div>
    
  </div>
  <div class="flex">
  <button class="resize-y rounded-md" action="#">
            <label for="search-field" class="sr-only">Search</label>
            <MagnifyingGlassIcon class="pointer-events-none absolute inset-y-0 left-0 h-full w-5 text-gray-400" aria-hidden="true" />
            <input id="search-field" class="block h- w-full border-0 py-0 pl-8 pr-0 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm" placeholder="Search..." type="search" name="search" />
          </button>
          <button type="button" class="relative ml-3 inline-flex items-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50">
          <EnvelopeIcon class="-ml-0.5 mr-1.5 h-5 w-5 text-gray-400" aria-hidden="true" />
          <span>Add Contact</span>
        </button>
        <CollectionsList
    :employeeDetails="contactsArray"
    @addEmployeeDetails="openAddContactsModal"
    @deleteContact="deleteModal"
    @editContact="editContacts"
  />

  <div v-if="is_modal" :key="render">
    <CollectionsAdd @employeeForm="employeeForm" />
  </div>
  <div v-if="is_edit" :key="render">
    <CollectionsEdit :employeeDetails="employeeDetail" />
  </div>
  <div v-if="is_delete" :key="render">
    <CollectionsDelete @deleteModal="deleteModal" />
  </div>
  </div>

  
</template>

<script setup lang="ts">
const is_modal = ref(false);
const render = ref(0);
const contactsArray = ref([]);
const is_edit = ref(false);
const is_delete = ref(false);
const employeeDetail = ref({});

const openAddContactsModal = () => {
  is_modal.value = true;
  render.value++;
};

onMounted(() => {
  const storedData = localStorage.getItem("formData");
  if (storedData) {
    contactsArray.value = JSON.parse(storedData);
  }
});

//Add employee Details Locally using Local Storage
const employeeForm = (data: any) => {
  contactsArray.value.push(data);
  localStorage.setItem("formData", JSON.stringify(contactsArray.value));
  is_modal.value = false;
};

//Edit Employee Locally
const editContacts = (empDetail, index) => {
  console.log(empDetail, index);
  employeeDetail.value = empDetail;
  render.value++;
  is_edit.value = true;
};

//Delete Employee Permanently
const deleteModal = (index: number) => {
  // is_delete.value = true;
  // render.value++;
  contactsArray.value.splice(index, 1);
  localStorage.setItem("formData", JSON.stringify(contactsArray.value));
};
</script>
