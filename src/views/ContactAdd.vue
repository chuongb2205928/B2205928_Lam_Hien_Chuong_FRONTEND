    <template>
    <div class="page">
        <h4>Thêm mới Liên hệ</h4>
        <ContactForm
        :contact="newContact"
        @submit:contact="createContact"
        />
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
            name: "",
            email: "",
            address: "",
            phone: "",
            favorite: false,
        },
        message: "",
        };
    },
    methods: {
        async createContact(contactData) {
        try {
            const created = await ContactService.create(contactData);
            alert("Liên hệ mới được tạo thành công!");
            // Chuyển về danh sách contact
            this.$router.push({ name: "contactbook" });
        } catch (error) {
            console.log(error);
            this.message = "Không thể tạo liên hệ. Vui lòng thử lại.";
        }
        },
    },
    };
    </script>
    <style scoped>
    .page {
    max-width: 750px;
    text-align: left;
    }
    </style>