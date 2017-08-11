<template>
<div id="app">
    <img src="./assets/logo.png">
    <t-adress @change="getAddr"></t-adress>

    <div class="container">
        <div class="title">Formdata 上传 demo</div>
        <!-- Document：https://developer.qiniu.com/kodo/manual/form-upload -->
        <form id="testform" method="post" enctype="multipart/form-data">
            <input name="key" id="key" type="hidden" value="">
            <input name="token" type="hidden" :value="uploadToken">
            <input id="userfile" name="file" type="file" @change="upload"/>
            <!-- take photo with phone -->
            <!-- <input id="userfile" name="file" accept="image/*" type="file" /> -->

            <!-- take video with phone -->
            <!-- <input id="userfile" name="file" type="file" accept="video/*"/> -->
            <input name="accept" type="hidden" />
        </form>

        <!-- add file -->
        <label for="userfile" class="trigger">
            <span>Trigger =></span>
            <em>添加文件</em>
        </label>

        <!-- upload info -->
        <div class="selected-file"></div>
        <div class="progress"></div>
        <div class="uploaded-result"></div>
    </div>
    <router-view></router-view>
</div>
</template>

<script>
import 'vue-address/lib/vue-address.min.css'
import TAdress from 'vue-address'
// import upload from './components/upload.vue'
export default {
    name: 'app',
    components: {
        TAdress,
        // upload
    },
    data: () => {
        return {
            uploadToken: 'FtFFvQIZOYBiPqSCA7dfdotzy-2uexcYJ3Pjxw9G:eL0jbS0IG-f71ww0ODI5qHqOn6U=:eyJzY29wZSI6InBhZG1vbSIsImRlYWRsaW5lIjoxNTAyNDQ5NjgxfQ=='
        }
    },
    methods: {
        getAddr(p, c, d) {
            console.log(p, c, d)
        },
        upload() {
            let f = new FormData(document.getElementById("testform"))
            console.log(f)
            this.$http.post('http://up-z2.qiniu.com/', f).then(function (res) {
                console.log('suceess')
                console.log(res)
            })
        },
    }
}
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

#select-address {
    display: block;
}

#select-address .stf-select {
    width: 200px;
    display: inline-block;
}
form {
    width: 200px;
    height: 200px;
    background-color: #ff9967;
    display: inline-block;
    position: relative;
    display: none;
}
form input[type="file"] {
    width: 100%;
    height: 100%;
    opacity: 0;
}
.trigger {
    border: 1px solid red;
    padding: 15px;
}
</style>
