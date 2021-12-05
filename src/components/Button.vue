<template>
    <button @click="onClick()" v-bind:style="{background: color}" class="btn">{{ text }}</button>
</template>

<script>
export default {
    name: "Button",
    props: {
        text: String,
        color: String
    },
    methods: {
        onClick() {
            // when the button is clicked, it emits the click event up to the parent component 
            this.$emit('btn-click');
        }
    }
}
</script>