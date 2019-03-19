<template>
<div class="container">
    <h1 class="text-center">Welcome to Chatire!</h1>
    <div id="auth-container" class="row">
        <div class="col-sm-4 offset-sm-4">
            <ul class="nav nav-tabs nav-justified" id="myTab" role="tablist">
                <li class="nav-item"><a href="#signup" class="nav-link active" id="signup-tab" data-toggle="tab" role="tab" aria-controls="signup" aria-selected="true">
                    Sign Up
                </a></li>
                <li class="nav-item"><a href="#signin" class="nav-link" id="signin-tab" data-toggle="tab" role="tab" aria-controls="signin" aria-selected="false">
                    Sign In
                </a></li>
            </ul>

            <div class="tab-content" id="myTabContent">
                <div class="tab-pane fade in show active" id="signup" role="tabpanel" aria-labelledby="signup-tab">
                    <form @submit.prevent="signUp">
                        <div class="form-group">
                            <input type="email" v-model="email" class="form-control" id="email" placeholder="Email Address" required>
                        </div>
                        <div class="form-row">
                            <div class="form-group col-md-6">
                                <input type="text" v-model="username" class="form-control" id="username" placeholder="Username" required>
                            </div>
                            <div class="form-group col-md-6">
                                <input type="password" v-model="password" class="form-control" id="password" placeholder="Password" required>
                            </div>
                        </div>
                        <div class="form-group">
                            <div class="form-check">
                                <input type="checkbox" class="form-check-input" id="toc" required>
                                <label for="gridCheck" class="form-check-label">
                                    Accept terms and Conditions
                                </label>
                            </div>
                        </div>
                        <button class="btn btn-block btn-primary" type="submit">Sign Up</button>
                    </form>
                </div>

                <div class="tab-pane fade" id="signin" role="tabpanel" aria-labelledby="signin-tab">
                    <form @submit.prevent="signIn">
                        <div class="form-group">
                            <input type="text" v-model="username" class="form-control" id="username" placeholder="Username">
                        </div>
                        <div class="form-group">
                            <input type="password" v-model="password" class="form-control" id="password" placeholder="Password" required>
                        </div>
                        <button class="btn btn-block btn-primary" type="submit">Sign In</button>
                    </form>
                </div>
            
            </div>

        </div>
    </div>        
</div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            email: '', username: '', password: ''
        }
    },
    methods: {
        signUpRoutine(user) {
            return new Promise((resolve, reject) => {
                axios({
                    url: 'http://localhost:8000/auth/users/create',
                    data: user,
                    method: 'POST'
                })
                .then((response) => {
                    alert('Your account has been created. You will be signed in automatically!');
                    resolve(response);
                })
                .catch((error) => {
                    reject(error);
                })
            });
            
        },
        signUp() {
            this.signUpRoutine({
                email: this.email, 
                username: this.username, 
                password: this.password}).then(() =>{
                this.signIn();
            })
            .catch(err => {
                console.log(err);
                console.log(err.data);
            });
        },
        signInRoutine(user) {
            return new Promise((resolve, reject) => {
                axios({
                    url: 'http://localhost:8000/auth/token/create',
                    data: user,
                    method: 'POST'
                })
                .then((response) => {
                    sessionStorage.setItem('authToken', response.data.auth_token);
                    sessionStorage.setItem('username',user.username)
                    console.log(user.username)
                    resolve(response);
                })
                .catch((error) => {
                    sessionStorage.removeItem('authToken');
                    reject(error);
                });
            })
            
        },
        signIn() {
            const {username, password} = this;
            this.signInRoutine({username, password}).then(() => {
                this.$router.push("/chat");
            })
            .catch(err => {
                console.log(err);
            });
        }
    }
};

</script>

<style scoped>
#auth-container {
    margin-top: 50px;
}

.tab-content {
    padding-top: 20px;
}
</style>

