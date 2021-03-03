<template>
    <div @click="favouriteTwoot(twoot.id)">
        <hr/>
        @{{ username }}
        <br/>
        {{ twoot.content }}
        <hr/>
    </div>
</template>

<script>
export default {
    name: 'TwootItem',
    props: {
        username: {
            type: String,
            required: true
        },
        twoot: {
            type: Object,
            required: true
        }
    },
    methods: {
        favouriteTwoot(id) {
            this.$emit('favourite', id);
        }
    }
};
</script>