<template>
    <div class="container__input">
        <component :is="renderIcon"/>
        <input type="text" :placeholder="placeholder" />
    </div>
</template>

<script>
import SearchIcon from './icons/SearchIcon.vue';
import PinIcon from './icons/PinIcon.vue';

export default {
    props: ['icon', 'placeholder'],
    components: {
        SearchIcon, 
        PinIcon
    },
    computed: {
        renderIcon: function () {
            const icons = {
                pin: PinIcon,
                search: SearchIcon
            }

            return icons[this.icon]
        }
    }
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

        input {
            outline: none;
            border: none;
            background: none;
        }
    }
}
</style>
  