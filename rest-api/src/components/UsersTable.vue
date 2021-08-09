<template>
    <div id="users-table">
        <!-- Conditional Message -->
        <div v-if="!users.length" class="alert alert-info" role="alert">
            There aren't users
        </div>
        <!-- Table -->
        <table class="table">
            <!-- Table Head -->
            <thead>
                <tr>
                    <th>
                        Name
                    </th>
                    <th>
                        Email
                    </th>
                    <th>
                        Actions
                    </th>
                </tr>
            </thead>
            <!-- Table Body -->
            <tbody>
                <!-- For Loop on Users List -->
                <tr v-for="user in users" :key="user.id">
                    <!-- Name -->
                    <td v-if="editing === user.id">
                        <input type="text" class="form-control" v-model="user.name">
                    </td>
                    <td v-else>
                        {{ user.name }}
                    </td>
                    <!-- Email -->
                    <td v-if="editing === user.id">
                        <input type="text" class="form-control" v-model="user.email">
                    </td>
                    <td v-else>
                        {{ user.email }}
                    </td>
                    <!-- Buttons -->
                    <td v-if="editing === user.id">
                        <button class="btn btn-success" @click="saveUser(user)">💾 Save</button>
                        <button class="btn btn-secundary ml-2" @click="cancelEdit(user)">❌ Cancel</button>
                    </td>
                    <td v-else>
                        <button class="btn btn-info" @click="editUser(user)">✏️ Edit</button>
                        <button class="btn btn-danger ml-2" @click="$emit('delete-user', user)">🗑️ Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'users-table',
    props: {
        users: Array,
    },
    data () {
        return {
            editing: null,
        }
    },
    methods: {
        editUser(user) {
            this.editedUser = Object.assign({}, user);
            this.editing = user.id;
        },
        saveUser(user) {
            if (!user.name.length || !user.email.length) {
                return;
            }
            this.$emit('update-user', user);
            this.editing = null;
        },
        cancelEdit(user) {
            Object.assign(user, this.editedUser);
            this.editing = null;
        }
    }
}
</script>