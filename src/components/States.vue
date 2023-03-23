<template>
    <div class="container__input">
        <SearchIcon />
        <select name="states" id="states" @change="$event => selectState($event.target.value)">
            <option selected>{{ placeholder }}</option>
            <option v-for="item in items" :key="item.name" :value="item.geonameId">{{ item.name }}</option>
        </select>
    </div>
</template>

<script>
import SearchIcon from './icons/SearchIcon.vue';

export default {
    props: {
        icon: String, 
        placeholder: String, 
        items: Array,
        selectState: Function
    },
    components: {
        SearchIcon,
    },
}
</script>

<style scoped lang="scss">

.container {
    &__input {
        display: flex;
        flex-direction: row;
        align-items: center;
        padding: 12px 8px 12px 14px;
        gap: 12px;
        margin-right: 12px;

        width: 348px;
        height: 48px;

        background: #F4F4FF;
        border-radius: 5px;

        input, select, option {
            outline: none;
            border: none;
            background: none;
            width: 100%;
        }
    }
}
</style>
  