<template>
    <div class="empty-list-container">
        <span v-if="keyword">
            The recepie list is empty. Please search for another recepie!
        </span>
        <span v-else>
            Start searching to find a new recepie!
        </span>
    </div>
</template>

<script>
export default {
    props: {
        keyword: {
            type: String,
            required: true
        }
    }
}
</script>

<style scoped>
.empty-list-container {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
}
</style>

