<template>
  <v-container fill-height>
      <v-layout justify-center row wrap>
          <v-flex xs12>
              <div class="mb-3">
                  <v-layout row wrap>
                      <v-flex>
                          <h1>Users</h1>
                      </v-flex>
                      <v-flex md4 xs12>
                          <v-spacer></v-spacer>
                          <v-text-field
                            v-model="search"
                            append-icon="search"
                            label="Search"
                            single-line
                            hide-details
                          ></v-text-field>
                      </v-flex>
                  </v-layout>
              </div>
              <v-data-table
                :headers="headers"
                :items="users"
                hide-actions
                class="elevation-1"
                :loading="loading"
                :search="search"
            >
                <template slot="items" slot-scope="{ item }">
                <td>{{ item.name }}</td>
                <td>{{ item.username }}</td>
                <td>{{ item.email }}</td>
                <td>{{ item.phone }}</td>
                <td>{{ item.website }}</td>
                <td>{{ item.company.name }}</td>
                </template>
            </v-data-table>
          </v-flex>
      </v-layout>
  </v-container>
</template>

<script>
export default {
    name: 'Users',
    data () {
        return {
            headers: [
                {
                    text: 'Name',
                    align: 'left',
                    value: 'name'
                },
                {
                    text: 'Username',
                    align: 'left',
                    value: 'username'
                },
                {
                    text: 'Email',
                    align: 'left',
                    value: 'email'
                },
                {
                    text: 'Phone',
                    align: 'left',
                    value: 'phone'
                },
                {
                    text: 'Website',
                    align: 'left',
                    value: 'website'
                },
                {
                    text: 'Company',
                    align: 'left',
                    value: 'company'
                }
            ],
            users: [],
            loading: false,
            search: ''
        }
    },
    created () {
        this.getUsers()
    },
    methods: {
        async getUsers () {
            try {
                this.loading = true
                const response = await axios.get('https://jsonplaceholder.typicode.com/users')
                this.users = response.data
            } catch (error) {
                console.log(error)
            } finally {
                this.loading = false
            }
        }
    }
}
</script>
