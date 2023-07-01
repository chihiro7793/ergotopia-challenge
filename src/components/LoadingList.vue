<template>
    <div class="loading-list">
        <b-spinner type="grow" label="Loading..."></b-spinner>
    </div>
</template>

<script>
export default {

}
</script>

<style>
.loading-list {
    height: 100%;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.loading-list span {
    background-color: #fe043d;
}
</style>

