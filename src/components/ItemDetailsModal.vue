<template>
    <b-modal v-if="details" scrollable size="lg" :visible="open" :title="`Details of ${details.title}`"
        @hide="$emit('close')" hide-footer>
        <p class="item-details-modal-body-title">
            <img src="~/assets/ingredients.png" />
            Ingredients:
        </p>
        <p v-for="(ingredient, index) in ingredients" :key="index">{{ ingredient }}</p>
        <hr />
        <p class="item-details-modal-body-title">
            <img src="~/assets/serving.png" />
            Servings:
        </p>
        <p> {{ details.servings }}</p>
        <hr />
        <p class="item-details-modal-body-title">
            <img src="~/assets/recepie.png" />
            Instructions:
        </p>
        <p>{{ details.instructions }}</p>
    </b-modal>
</template>

<script>

export default {
    props: {
        open: {
            type: Boolean,
            required: true,
        },
        details: {
            type: Object,
            default: null
        }
    },

    computed: {
        ingredients() {
            return this.details.ingredients.split('|') || '-'
        }
    }

};
</script>

<style>
.item-details-modal-body-title {
    font-weight: 600;
    font-size: 1.1rem;
}

.item-details-modal-body-title img {
    width: 24px;
    height: 24px;
}
</style>
