<template>
    <div>
        <div :class="'alert-' + type" class="alert alert-dismissible fade show" role="alert">
            <button v-if="closable" type="button" class="close" data-dismiss="alert" aria-label="Close">
                <span aria-hidden="true">&times;</span>
            </button>
            {{ message }}
        </div>
    </div>
</template>

<script>
    export default {
        name: "Alert",
        props: {
            message: {
                type: String,
                required: true,
                default: "Your message goes here!"
            },
            type: {
                type: String,
                default: 'info'
            },
            closable: {
                type: Boolean,
                default: false
            }
        }
    }
</script>