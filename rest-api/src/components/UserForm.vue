<template>
    <div id="user-form">
        <!-- Form -->
        <form @submit.prevent="sendForm">
            <!-- Container #1 -->
            <div class="container">
                <!-- Row #1 -->
                <div class="row">
                    <!-- Column #1 -->
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Name</label>
                            <input 
                                ref="name" 
                                v-model="user.name" 
                                type="text" 
                                class="form-control"
                                :class="{ 'is-invalid': process && invalidName }"
                                @focus="resetState"
                                @keypress="resetState"
                            >
                        </div>
                    </div>
                    <!-- Column #2 -->
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Email</label>
                            <input 
                                v-model="user.email" 
                                type="email" 
                                class="form-control"
                                :class="{ 'is-invalid': process && invalidEmail }"
                                @focus="resetState"
                            >
                        </div>
                    </div>
                </div>
                <!-- Row #2 -->
                <div class="row">
                    <!-- Column #1  -->
                    <div class="col-md-4">
                        <div class="form-group">
                            <button class="btn btn-primary">Add User</button>
                        </div>
                    </div>
                </div>
            </div>
            <!-- Container #2 -->
            <div class="container">
                <!-- Row #1 -->
                <div class="row">
                    <!-- Column #1 -->
                    <div class="col-md-12">
                        <div v-if="error && process" class="alert alert-danger" role="alert">
                            You must fill all the fields!
                        </div>
                        <div v-if="correct" class="alert alert-success" role="alert">
                            The user has been added successfully!
                        </div>
                    </div>
                </div>
            </div>
        </form>
    </div>

</template>

<script>
export default {
    name: 'user-form', 
    data () {
        return {
            process: false,
            correct: false,
            error: false,
            user: {
                name: '',
                email: '',
            }
        }
    },
    methods: {
        sendForm() {
            this.process = true;
            this.resetStatus();
            // We check for errors
            if (this.invalidName || this.invalidEmail) {
                this.error = true;
                return;
            }

            this.$emit('create-user', this.user);
            this.$refs.name.focus();
            this.error = false;
            this.correct = true;
            this.process = false;

            // We reset the value of the variables
            this.user = {
                name: '', 
                email: '',
            }
        },
        resetStatus() {
            this.correct = false;
            this.error = false;
        }
    },
    computed: {
        invalidName() {
            return this.user.name.length < 1;
        },
        invalidEmail() {
            return this.user.email.length < 1;
        },
    },
}
</script>