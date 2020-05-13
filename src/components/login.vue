<template>
<div class="flex justify-center">
    <div class="w-full max-w-xs">
        <form @submit.prevent="login" class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
            <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="email">
                    Email
                </label>
                <input v-model="email"  v-bind:class="{ ' mb-3 border-red-500 ': emailHasError }" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Email">
                <p class="text-red-500 text-xs italic" >{{ alertEmail }}</p>
            </div>
            <div class="mb-6">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                    Password
                </label>
                <input v-model="password"  v-bind:class="{ ' mb-3 border-red-500 ': passwordHasError }" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" placeholder="******************">
                <p class="text-red-500 text-xs italic" >{{ alertPassword }}</p>
            </div>
            <div class="flex items-center justify-between">
                <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                    Sign In
                </button>
                <a class="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800" href="#">
                    Forgot Password?
                </a>
            </div>
        </form>
        <p class="text-center text-gray-500 text-xs">
            &copy;2020 Sahabat Studio. All rights reserved.
        </p>
    </div>
</div>
</template>

<script>
import axios from 'axios'
import Cookies from 'js-cookie'

export default {
  name: 'Login.vue',

  data: () => ({
    email : '',
    password : '',
    alertPassword : '',
    alertEmail : '',
    emailHasError : false,
    passwordHasError : false
  }),

  mounted() {

  },

  methods:{
    async login() {
        await axios.post('http://deskrelawan-api.test/login', {
            email : this.email,
            password : this.password
        })
        .then(response => {
            if (response.status == 200) {
                const apiToken = response.data.result.api_token;
                Cookies.set('token', apiToken);
                this.$router.push('/')
            }
        })
        .catch(err => {
            console.log(err);
            if (err.response.status == 401) {
                const error = err.response.data.error;
                if ( error.email ){
                    this.alertEmail = error.email[0];
                    this.emailHasError = true;
                }else{
                    this.alertEmail = '';
                    this.emailHasError = false;
                }
                if ( error.password ){
                    this.alertPassword = error.password[0];
                    this.passwordHasError = true;
                }else{
                    this.alertEmail = '';
                    this.emailHasError = false;
                }
            }
        })
    }
  }

}
</script>