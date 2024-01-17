<template>
  <!DOCTYPE html>
    <html lang="en">
        <head>
            <meta charset="UTF-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0" />
            <title>Login Page</title>
            <!-- 引入 Bootstrap 5 CSS -->
            <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous" />
        </head>
        <body>
            <div class="container mt-5">
                <div class="row justify-content-center">
                    <div class="col-md-6">
                        <div class="card">
                            <div class="card-header">
                                <h3 class="text-center">登入</h3>
                            </div>
                            <div class="card-body">
                                <form @submit.prevent="login">
                                    <div class="mb-3">
                                        <label for="username" class="form-label">使用者名稱：</label>
                                        <input type="text" class="form-control" v-model="user.username" id="username" name="username" required />
                                    </div>
                                    <div class="mb-3">
                                        <label for="password" class="form-label">密碼：</label>
                                        <input type="password" class="form-control" name="password" v-model="user.password" autocomplete="current-password" />
                                    </div>
                                    <div class="mb-3 form-check">
                                        <input type="checkbox" class="form-check-input" id="rememberMe" />
                                        <label class="form-check-label" for="rememberMe">記住我</label>
                                    </div>
                                    <div class="text-center">
                                        <button type="submit" class="btn btn-primary">登入</button>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </body>
    </html>
</template>


<script>
import axios from "axios";

export default {
    name: "HomeView",
    components: {},
    data() {
        return {
            user: {
                username: "",
                password: "",
            },
        };
    },
    methods: {
        login() {
            const api = "https://vue3-course-api.hexschool.io/v2/admin/signin";
            axios
                .post(api, this.user)
                .then((response) => {
                    const { token, expired } = response.data;
                    console.log(response);
                    document.cookie = `hexToken=${token};expires=${new Date(expired)}; path=/`;
                    this.$router.push('/product')

                })
                .catch((err) => {
                    alert(err.response.data.message);
                });
        },
    },
};
</script>

