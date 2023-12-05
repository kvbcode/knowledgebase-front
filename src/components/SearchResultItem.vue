<template>
    <div class="search-item">
        <a :href="src.location" target="_blank">
        <div class="item-title">{{ src.title }}</div>
        <div class="item-header">{{ getModified }} {{ src.header }}</div>
        </a>
    </div>
</template>

<script>
export default{
    props: {
        src: {
            type: Object,
            require: true
        }
    },
    computed: {
        getModified: function(){
            const dt = new Date(this.src.modified);
            return dt.toLocaleDateString();
        }
    }
}
</script>

<style scoped>
.search-item {
    height: 24pt;
    margin: 5px
}
.item-title {
    font-size: 12pt;
    font-weight: bold;
}
.item-header {
    font-size: 10pt;
}
a {
    text-decoration: none;
    color: inherit;
}
</style>