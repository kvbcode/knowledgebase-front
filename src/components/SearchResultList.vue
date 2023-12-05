
<template>
    <div v-cloak class="d-grid gap-2">
        <div v-for="item in items" :key="item.id" class="p-2 bg-light border">
            <SearchResultItem :src="item"></SearchResultItem>
        </div>
    </div>
</template>

<script>
import SearchResultItem from './SearchResultItem.vue';

export default {
    components: {
        SearchResultItem
    },
    props: {
        items: {
            type: Array,
            required: true
        }
    }
}

</script>