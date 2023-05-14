


<template>
    <div class="container mx-auto p-8 bg-white shadow-lg rounded-lg">
      <div class="flex flex-col items-center">
        <img src="../public/logo.png" class="rounded-full w-20 h-20 mb-4" alt="Logo" />
        <h1 class="text-2xl font-bold mb-4">ApplAI</h1>
      </div>
  
      <div class="flex flex-col space-y-4">
        <label for="name" class="text-lg font-medium">Name</label>
        <input v-model="form.name" type="text" id="name" class="p-2 border border-gray-300 rounded" />
  
        <label for="phone" class="text-lg font-medium">Phone Number</label>
        <input v-model="form.phone" type="tel" id="phone" class="p-2 border border-gray-300 rounded" />
  
        <label for="email" class="text-lg font-medium">Email</label>
        <input v-model="form.email" type="email" id="email" class="p-2 border border-gray-300 rounded" />
  
        <label for="cv" class="text-lg font-medium">CV</label>
        <input @change="onFileChange" type="file" id="cv" class="p-2 border border-gray-300 rounded" />
  
        <button @click="saveFile" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-4">Save</button>
  
        <label for="template" class="text-lg font-medium">Application Template</label>
        <textarea v-model="form.template" id="template" class="p-2 border border-gray-300 rounded"></textarea>
        <button v-show="isApplyVisible" @click="apply" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded mt-4">Apply</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        phone: '',
        email: '',
        cv: null,
        template: '',
      },
      currentURL: window.location.href,
    };
  },
  computed: {
    isApplyVisible() {
      const regex = /^https:\/\/www\.finn\.no\/job\/fulltime\/ad\.html\?finnkode=/;
      return regex.test(this.currentURL);
    },
  },
  created() {
    this.checkApplyVisibility();
  },
  methods: {
    checkApplyVisibility() {
      chrome.tabs.query({ active: true, currentWindow: true }, (tabs) => {
        const currentURL = tabs[0].url;
        console.log('currentURL:', currentURL);
        this.currentURL = currentURL; // Update the currentURL data property
      });
    },
    onFileChange(e) {
      this.form.cv = e.target.files[0];
    },
    saveFile() {
      // Your logic to handle file save
    },
    apply() {
      // Your logic to handle form submission
    },
  },
};
</script>
