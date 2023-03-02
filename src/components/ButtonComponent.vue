<template>
    <button class="button">
        {{ label }}
    </button>
</template>

<script>
export default {
    props: ['label'],
}
</script>

<style scoped lang="scss">

.button {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 12px 32px;
    gap: 8px;
    outline: none;
    border: none;

    background: var(--primary);
    border-radius: 5px;
    color: var(--vt-c-white);
}
</style>