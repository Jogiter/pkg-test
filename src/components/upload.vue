<template>
    <div>
        <form :id="formId" :method="method" enctype="multipart/form-data">
            <slot name="form">
                <input name="token" type="hidden" :value="token">
                <input name="file" :id="pickerId" type="file" @change="upload" :accept="accept"/>
                <input name="accept" type="hidden" />
            </slot>
        </form>

        <!-- add file -->
        <label :for="pickerId">
            <slot name="picker">
                <em>添加文件</em>
            </slot>
        </label>
    </div>
</template>

<script>
    export default {
        props: {
            method: {
                type: String,
                default: 'post'
            },
            action: {
                type: String,
                default: ''
            },
            token: {
                type: String,
                default: ''
            },
            accept: {
                type: String,
                default: 'image/*'
            },
            callback: {
                type: Function,
                default: () => {
                    console.log('upload done');
                }
            }
        },
        data: function () {
            return {
                key: '',
                formId: `upload${new Date().getTime()}`,
                pickerId: `picker${new Date().getTime()}`
            }
        },
        methods: {
            upload() {
                this.key = Math.random().toString(36).substr(2) + document.getElementById(this.pickerId).value.match(/\.?[^.\/]+$/)
                this.$nextTick(() => {
                    let formData = new FormData(document.getElementById(this.formId))
                    this.$http.post(this.action, formData).then(res => {
                        this.$emit('on-upload', res.body)
                    })
                })
            }
        }
    }
</script>

<style scoped>
    form {
        display: none;
    }
</style>
