<template>
    <div class="button-wrapper">
        <ElButton class="button-positive" type="success" @click="onClickPositive">Show Income</ElButton>
        <ElButton class="button-negative" type="danger" @click="onClickNegative">Show Outcome</ElButton>
        <ElButton class="button-all" type="info" @click="onClickAll">Show all</ElButton>
    </div>
</template>

<script>
export default {
    name: 'SortButtons',
    methods: {
        onClickPositive() {
            this.$emit('showPositive');
        },
        onClickNegative() {
            this.$emit('showNegative');
        },
        onClickAll() {
            this.$emit('showAll');
        }
    }
}
</script>

<style scoped>
.button-wrapper {
    margin: 20px 0;
}

</style>