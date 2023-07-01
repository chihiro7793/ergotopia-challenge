<template>
    <b-card tag="div" class="search-card-container border-0" body-class="search-card-body">
        <div class="search-card-input-container">
            <search-input v-model="keyword" input-id="search-input" label="Search recepies" />
            <hr />
        </div>
        <div class="search-card-list-container">
            <div class="w-100 h-100" v-if="!loading && keyword">
                <search-list :recepies="recepies" />
                <div class="search-card-list-pagination mt-2 d-flex justify-content-center">
                    <button :disabled="isDisabled('back')" @click="handlePagination('back')">
                        <b-icon icon='caret-left-fill' style="width: 24px; height: 24px;color: #fe043d;" />
                    </button>
                    <button :disabled="isDisabled('next')" @click="handlePagination('next')">
                        <b-icon icon='caret-right-fill' style="width: 24px; height: 24px;color: #fe043d;" />
                    </button>
                </div>
            </div>
            <empty-list :keyword="keyword" v-else-if="!loading && !keyword" />
            <div class="w-100  h-100" v-else-if="loading">
                <loading-list />
            </div>
        </div>
    </b-card>
</template>

<script>
import SearchInput from './SearchInput.vue'
import SearchList from './SearchList.vue';
import EmptyList from './EmptyList.vue';
import LoadingList from './LoadingList.vue';


const MAX_PAGE_NUM = 5;
const DEFAULT_PAGE_SIZE = 10;
export default {
    components: {
        SearchInput,
        SearchList,
        EmptyList,
        LoadingList
    },
    data() {
        return {
            recepies: [],
            keyword: '',
            page: 0,
            pageSize: DEFAULT_PAGE_SIZE,
            loading: false,
            debounceTimeout: null
        }
    },
    created() {
        if (this.keyword) {
            this.fetchRecpies(this.keyword, this.offset)
        }
    },
    computed: {
        offset() {
            return this.page * this.pageSize + this.pageSize;
        }
    },
    methods: {
        fetchRecpies(query, offset) {
            this.loading = true;
            fetch(`https://api.api-ninjas.com/v1/recipe?query=${query}&offset=${offset}`, {
                method: 'GET',
                headers: { 'X-Api-Key': process.env.API_KEY },
                contentType: 'application/json',
            })
                .then(response => response.json())
                .then(resp => {
                    this.loading = false;
                    this.recepies = [...resp];
                })
                .catch(err => {
                    console.log(err)
                })
        },
        isDisabled(value) {
            switch (value) {
                case 'back':
                    return this.page === 0 || !this.recepies.length
                case 'next':
                    return this.page === MAX_PAGE_NUM || !this.recepies.length;
                default:
                    return false;
            }
        },
        handlePagination(value) {
            if (value === 'back' && this.page !== 0) {
                this.page--;
            }
            if (value === 'next' && this.page !== MAX_PAGE_NUM) {
                this.page++;
            }
        }
    },
    watch: {
        keyword(value) {
            this.page = 0;
            if (value) {
                if (this.debounceTimeout) {
                    clearTimeout(this.debounceTimeout);
                }
                this.debounceTimeout = setTimeout(() => {
                    this.fetchRecpies(value, this.offset)
                }, 1000);
            }
        },
        page() {
            this.fetchRecpies(this.keyword, this.offset)
        }
    }
}
</script>

<style>
.search-card-container {
    display: flex;
    min-width: 50%;
    height: 90%;
    background: #e8e8e8;
}

.search-card-list-container {
    height: 80%;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.search-card-body {
    display: flex;
    flex-direction: column;
    height: 100%;
}

.search-card-list-pagination {
    height: 24px;
}

.search-card-list-pagination button {
    background: none;
    color: inherit;
    border: none;
    padding: 0;
    font: inherit;
    cursor: pointer;
    outline: inherit;
}

.search-card-list-pagination button:disabled>svg {
    cursor: default;
    fill: gray
}
</style>