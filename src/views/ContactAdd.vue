<template>
    <div class="page">
      <h4>Thêm Liên hệ</h4>
      <ContactForm @submit:contact="addContact" :contact="newContact" />
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import ContactForm from "@/components/ContactForm.vue";
  import ContactService from "@/services/contact.service";
  
  export default {
    components: {
      ContactForm,
    },
    data() {
      return {
        newContact: {
          name: '',
          email: '',
          address: '',
          phone: '',
          favorite: false
        },
        message: "",
      };
    },
    methods: {
      async addContact(data) {
        try {
          await ContactService.create(data);
          this.message = "Liên hệ được thêm mới thành công.";
        } catch (error) {
          console.log(error);
          // Xử lý lỗi
          this.$router.push({
            name: "notfound",
            params: {
              pathMatch: this.$route.path.split("/").slice(1),
            },
            query: this.$route.query,
            hash: this.$route.hash,
          });
        }
      },
    },
  };
  </script>
  