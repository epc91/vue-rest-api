<template>
    <div id="users-table">
        <div v-if="!users.length" class="alert alert-info" role="alert">
            There are't users
        </div>
        <table class="table">
            <thead>
                <tr>
                    <th>
                        Name
                    </th>
                    <th>
                        Email
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in users" :key="user.id">
                    <td> {{ user.name }} </td>
                    <td> {{ user.email }} </td>
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
}
</script>