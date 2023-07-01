<template>
    <div class="search-list-container">
        <ul v-if="recepies.length" class="search-list-ul">
            <li class="search-list-li" v-for="(recepie, index) in recepies" :key="index" @click="selectRecepie(recepie)">
                {{ recepie.title }}
            </li>
        </ul>
        <div v-else>Search List is Empty!</div>
        <item-details-modal :details="selectedRecepie" :open="isDetailModalOpen" @close="closeModal" />
    </div>
</template>

<script>
import { BIcon } from 'bootstrap-vue'
import ItemDetailsModal from './ItemDetailsModal.vue';
export default {
    components: {
        ItemDetailsModal,
        BIcon
    },
    props: {
        recepies: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            isDetailModalOpen: false,
            selectedRecepie: null
        }
    },
    methods: {
        selectRecepie(recepie) {
            this.selectedRecepie = recepie;
            this.isDetailModalOpen = true;
        },
        closeModal() {
            this.selectedRecepie = null;
            this.isDetailModalOpen = false;
        }
    }
}
</script>

<style>
.search-list-container {
    height: 100%;
    overflow: auto;
}

.search-list-ul {
    list-style-type: none;
    padding: 0;
    width: 100%;
}

.search-list-li {
    font-size: 1rem;
    cursor: pointer;
    padding: 8px;
}

.search-list-li:nth-child(odd) {
    background-color: #f2f2f2;
}

.search-list-li:nth-child(even) {
    background-color: #ccc;
}

.search-list-li:hover:nth-child(odd) {
    background-color: #d9d9d9;
    ;
}

.search-list-li:hover:nth-child(even) {
    background-color: #b3b3b3
}

.search-list-li:first-child {
    border-radius: 5px 5px 0 0;
}

.search-list-li:last-child {
    border-radius: 0 0 5px 5px;
}
</style>