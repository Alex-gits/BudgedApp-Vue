<template>
    <div class="budget-list-wrap">
        <template v-if="isEmpty">
            <ElCard :header="header">
                <SortButtons @showPositive="onClickPositive" @showNegative="onClickNegative" @showAll="onClickAll"/>
                <BudgetItem :list="list" @initDelete="deleteItem"/>
            </ElCard>
        </template>
        <ElAlert v-else :title="emptyTitle" type="info" :closable="false"/>
    </div>
</template>

<script>
import BudgetItem from '@/components/BudgetItem';
import SortButtons from '@/components/SortButtons';

export default {
    name: 'BudgetList',
    components: {
        BudgetItem,
        SortButtons
    },
    props: {
        list: {
            type: Object,
            default: () => ({}),
        },
    },
    data: () => ({
        header: 'Budget List',
        emptyTitle: 'Empty list',
    }),
    computed: {
        isEmpty() {
            return Boolean(Object.keys(this.list).length);
        }
    },
    methods: {
        deleteItem(id) {
            this.$emit('deleteItem', id);
        },
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
.budget-list-wrap {
    max-width: 500px;
    margin: auto;
}
</style>