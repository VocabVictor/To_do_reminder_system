<template>
    <!--DengLuhtmlStart-->
    <el-row>


    </el-row>
    <!--DengLuhtmlEnd-->

</template>

<script>
    export default {
        name: 'Login',
        data() {
            return {
                //DengLujsStart
                //DengLujsEnd
            }
        },
        methods: {
            //DengLumethodsStart
            //DengLumethodsEnd
        },
        mounted() {
            //DengLumountedStart
            //DengLumountedEnd
        }
    }
</script>

<style rel="stylesheet/scss" lang="scss">
    .DengLucssStart {}

    .top {
        display: block;
        position: relative;
        font-size: 12px;
        color: rgb(51, 51, 51);
        text-align: start;
        line-height: 20px;
        left: 0px;
        top: 0px;
        right: 0px;
        bottom: 0px;
    }

    .background {
        display: block;
        background-image: url(../assets/images/entrance_bg.jpg);
        position: relative;
        font-size: 12px;
        color: rgb(51, 51, 51);
        text-align: start;
        background-color: rgb(128, 128, 128);
        line-height: 20px;
        left: 0px;
        top: 0px;
        right: 0px;
        bottom: 0px;
        background-repeat: repeat-x;
    }

    .bottom {
        display: block;
        height: inherit;
        position: absolute;
        font-size: 12px;
        color: rgb(255, 255, 255);
        text-align: center;
        background-color: rgb(108, 33, 166);
        line-height: 60px;
        left: 0px;
        top: 731.333px;
        right: 0px;
        bottom: 0px;
        box-sizing: content-box;
    }

    @media (min-width: 576px) {}

    @media (min-width: 768px) {}

    @media (min-width: 992px) {}

    @media (min-width: 1200px) {}

    .DengLucssEnd {}
</style>



// DengLuDataStart

redirect:undefined,
loginForm:{"username":"admin","password":"admin123","rememberMe":false,"code":"","uuid":""},
loginRules:{"username":[{"required":true,"trigger":"blur","message":"请输入您的账号"}],"password":[{"required":true,"trigger":"blur","message":"请输入您的密码"}],"code":[{"required":true,"trigger":"change","message":"请输入验证码"}]},
captchaEnabled:true,
codeUrl:'',
loading:false
// DengLuDataEnd
// DengLuMethodStart
// getCookie
getCookie(){


const username = Cookies.get("username");
const password = Cookies.get("password");
const rememberMe = Cookies.get('rememberMe')
this.loginForm = {
username: username === undefined ? this.loginForm.username : username,
password: password === undefined ? this.loginForm.password : decrypt(password),
rememberMe: rememberMe === undefined ? false : Boolean(rememberMe)
};


},// handleLogin
handleLogin(){


this.$refs.loginForm.validate(valid => {
if (valid) {
this.loading = true;
if (this.loginForm.rememberMe) {
Cookies.set("username", this.loginForm.username, {
expires: 30
});
Cookies.set("password", encrypt(this.loginForm.password), {
expires: 30
});
Cookies.set('rememberMe', this.loginForm.rememberMe, {
expires: 30
});
} else {
Cookies.remove("username");
Cookies.remove("password");
Cookies.remove('rememberMe');
}
this.$store.dispatch("Login", this.loginForm).then(() => {
this.$router.push({
path: this.redirect || "/"
}).catch(() => {});
}).catch(() => {
this.loading = false;
if (this.captchaEnabled) {
this.getCode();
}
});
}
});


},// getCode
getCode(){


getCodeImg().then(res => {
this.captchaEnabled = res.captchaEnabled === undefined ? true : res.captchaEnabled;
if (this.captchaEnabled) {
this.codeUrl = "data:image/gif;base64," + res.img;
this.loginForm.uuid = res.uuid;
}
});


}
// DengLuMethodEnd
// DengLuMountedStart

// DengLuMountedEnd
