

<template>

    <div id="container">
        <div id="left">
            <h1 id="welcome">Welcome</h1>
            <p id="lorem">
                Only Admin login.<br>
                To play Quiz Visit the link below<br>
                <router-link to="/">Play QUIZ </router-link><br>
                Test Your Knowledge<br>
                All the Best!!
            </p>
        </div>
        <div id="right">
            <h1 id="login">LogIn</h1><br>
            <input type="email" v-model="user.user_id" id="email" class="client-info">
            <label for="email">Email</label>
            <input type="password" v-model="user.user_password" id="password" class="client-info">
            <label for="password">Password</label>
            <input type="submit" id="submit" class="client-info" v-on:click.prevent="login" value="Submit">

        </div>
    </div>


</template>

<script>

export default {
    data() {
        return {
            user: {},
            status: false,
            msg: ''
        }
    },
    methods: {
        login: function () {
            this.$http.post('http://localhost:3000/user/login', this.user
            ).then(function (data) {
                console.log(data.body.tokens.refreshtoken)
                this.$session.start();
                this.$session.set("token", data.body.tokens.refreshtoken);

                this.$router.push('/dashboard');
            }).catch(function (error) {
                console.log(error)
            })

        }
    }

}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    outline: none;
}

:root {
    --main-color: #fff;
    --second-color: #347deb;
    --box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);

}

html {
    height: 100%;
}

body {
    background-image: linear-gradient(310deg, #df98fa, #9055ff);
    font-family: sans-serif;
}

#container {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    background-color: var(--main-color);
    width: 1200px;
    height: 800px;
    border-radius: 10px;
    display: grid;
    grid-template-columns: repeat(2, 50%);
    box-shadow: var(--box-shadow);
    transition-duration: 1s;
}

#left,
#right {
    margin: auto;
    width: 95%;
    height: 96%;
    border-radius: 10px;
}

#left {
    background-image: url("https://images.unsplash.com/photo-1615400014497-55726234cccb?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxNDU4OXwwfDF8cmFuZG9tfHx8fHx8fHx8MTYxNzg4Njg0Ng&ixlib=rb-1.2.1&q=85");
    background-size: cover;
    background-position: center;
    box-shadow: var(--box-shadow);
}

#welcome,
#lorem {
    margin: 20px;
    text-shadow: var(--box-shadow);
}

#welcome {
    font-size: 75px;
    font-weight: 300;
    margin-top: 330px;
    text-shadow: var(--box-shadow);
}

#login {
    padding-top: 35%;
    text-align: center;
    text-transform: uppercase;
    font-weight: 100;
    text-shadow: var(--box-shadow);
}

.client-info {
    display: block;
    margin: 20px auto;
    width: 60%;
    height: 50px;
    border: solid #999 1px;
    border-radius: 5px;
    text-indent: 15px;
    transition: all 200ms;
    box-shadow: var(--box-shadow);
}

.client-info:focus {
    width: 80%;
}

label {
    position: absolute;
    margin: -76px 130px;
    font-size: 12px;
    white-space: nowrap;
    background: #fff;
    padding: 0 5px;
    color: #999;
    transition: all 200ms;
    text-shadow: var(--box-shadow);
}

#email:focus~label[for="email"] {
    margin: -76px 70px;
}

#password:focus~label[for="password"] {
    margin: -76px 70px;
}

#submit {
    border: none;
    background-color: #9055ff;
    color: white;
    width: 60%;
}

#submit:hover {
    background-color: #df98fa;
}

@media (max-width: 1250px) {

    #container {
        width: 600px;
        display: block;
    }

    #left {
        display: none;
    }

    #right {
        margin-top: 16px;
        background-image: url("https://images.unsplash.com/photo-1615400014497-55726234cccb?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxNDU4OXwwfDF8cmFuZG9tfHx8fHx8fHx8MTYxNzg4Njg0Ng&ixlib=rb-1.2.1&q=85");
        background-size: cover;
        background-position: center;
        box-shadow: var(--box-shadow);
    }

}

@media (max-height: 850px) {

    #container {
        width: 1000px;
        height: 600px;
    }

    #login {
        padding-top: 20%;
    }

    #welcome {
        margin-top: 240px;
        font-size: 60px;
    }

    #lorem {
        font-size: 15px;
    }

}
</style>
