<script>
export default {
    name: 'Search Bar',
    data: () => ({ searchWord: '' }),
    props: {
        placeholder: String,
        buttonLabel: String
    },
    emits: ['form-submit', 'writing']
}
</script>

<template>
    <!-- # Search Bar -->
    <form @submit.prevent="$emit('form-submit')">
        <input type="text" :placeholder="placeholder || 'Cerca...'" v-model.trim="searchWord"
            @keyup="$emit('writing', searchWord)">
        <button>{{ buttonLabel || 'Cerca' }}</button>
    </form>
</template>

<style scoped>
button {
    background-color: red;
    color: #fff;
}
</style>