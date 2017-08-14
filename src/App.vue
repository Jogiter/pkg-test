<template>
<div id="app">
    <img src="./assets/logo.png">
    <t-adress @change="getAddr"></t-adress>

    <div class="container">
        <div class="title">Formdata 上传 demo</div>
        <!-- Document：https://developer.qiniu.com/kodo/manual/form-upload -->

        <upload :action="action" :token="token" @on-upload="uploadImg" :accept="accept">
            <p slot="picker" class="upload-btn">
                <span>上传图片</span>
            </p>
        </upload>

        <div class="block">
            <div id="result">
                <p>{{hash}}</p>
                <p>{{key}}</p>
            </div>
            <img :src="imgHash" alt="" class="viewimg">
            <img :src="imgKey" alt="" class="viewimg">
        </div>
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
import upload from './components/upload.vue'
export default {
    name: 'app',
    components: {
        TAdress,
        upload
    },
    data: () => {
        return {
            action: 'http://up-z2.qiniu.com/',
            // action: 'http://upload.qiniu.com/',
            accept: 'image/*',
            token: 'FtFFvQIZOYBiPqSCA7dfdotzy-2uexcYJ3Pjxw9G:UxuBHs_reBxKeMICvw0sQAgiMoM=:eyJzY29wZSI6InBhZG1vbSIsImRlYWRsaW5lIjoxNTAyNjk4MjIzfQ==',
            hash: '',
            key: ''
        }
    },
    computed: {
        imgHash: function () {
            return `http://img.padmom.com/${this.hash}`
        },
        imgKey: function () {
            return `http://img.padmom.com/${this.key}`
        }
    },
    methods: {
        getAddr(p, c, d) {
            console.log(p, c, d)
        },
        uploadImg(res) {
            this.hash = res.hash
            this.key = res.key
        }
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
.block,
.viewimg {
    margin: 15px;
}
.viewimg {
    max-width: 200px;
}
</style>
