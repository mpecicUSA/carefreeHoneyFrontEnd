<template>
    <v-container>
    <form>
        <v-text-field
        v-model="email"
        label="E-mail"
        required
        ></v-text-field>
        <v-text-field
        v-model="password"
        label="Password"
        type="password"
        required
        ></v-text-field>
        <v-layout>
            <v-flex xs6>
            <v-btn route to="/register">Register</v-btn>
            </v-flex>
            <v-flex xs6>
            <v-spacer></v-spacer>
            <v-btn color="orange" @click="submit" >Submit</v-btn>
            <v-btn color="error" @click="clear" >Clear</v-btn>
            </v-flex>
        </v-layout>
    </form>
    </v-container>
</template>




<script>
import axios from "axios"
    export default {
    data: () => ({
        email: '',
        password: ''
    }),

    methods: {
        submit () {
            axios.post('http://localhost:8000/login', {
                email:this.email,
                password:this.password
            })
            .then(res => {
                this.$store.state.user = {'token': res.data.token,'user_id': res.data.user.id,'firstName': res.data.user.firstName, "admin": res.data.user.admin},
                this.$store.state.isLoggedIn = true,
                this.$router.push('/')
            })
            .catch(err => {
            console.error(err);
            alert('Error logging in please try again');
            });
            axios.get(`http://localhost:8000/purchases/${res.data.user.id}`)
                .then( res => {
                    this.$store.state.purchases = res
                })
                .catch((err) => {
                    console.log(err)
                    alert('Error getting purchases')
                })
        },
        clear () {
            this.email = '',
            this.password = ''
        }
    }
}
</script>
