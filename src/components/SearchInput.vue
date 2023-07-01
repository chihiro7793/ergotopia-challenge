<template>
    <b-row class="my-1 align-items-center">
        <b-col sm="3" class="pr-0">
            <label :for="inputId" class="search-input-label">{{ label }}</label>
        </b-col>
        <b-col sm="9" class="pl-0">
            <input :id="inputId" type="text" :value="keyword" @input="$emit('input', $event.target.value)"
                class="search-input-box" />
        </b-col>
    </b-row>
</template>


<script>

export default {
    props: {
        keyword: {
            type: String,
            default: ''
        },
        label: {
            type: String,
            default: 'Search'
        },
        inputId: {
            type: String,
            required: true
        }
    }
}
</script>

<style>
.search-input-label {
    font-size: 0.75rem;
}

.search-input-box {
    display: block;
    width: 100%;
    height: calc(1.5em + 0.75rem + 2px);
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.search-input-box:focus {
    color: #495057;
    background-color: #fff;
    border-color: #80bdff;
    outline: none !important;
    border: 1px solid #fe043d;
    box-shadow: 0 0 0 0.2rem #fe043e13;
}
</style>