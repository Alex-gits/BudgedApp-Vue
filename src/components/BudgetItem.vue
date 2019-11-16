<template>
    <div>
        <div class="list-item" v-for="(item, prop) in list" :key="prop" :data-atr="item.id">
            <template v-if="item.value > 0">
                <span class="budget-comment">{{ item.comment }} <i class="el-icon-top"></i></span>
                <span class="budget-value item-green"> {{ item.value }} </span>
            </template>
            <template v-else>
                <span class="budget-comment">{{ item.comment }} <i class="el-icon-bottom"></i></span>
                <span class="budget-value item-red">{{ item.value }}</span>
            </template>
            <DeleteModal :dialogVisible="dialogVisible" @closed="closeModal" @initDelete="deleteItem"/>
            <ElButton type="danger" size="mini" @click="openDialog(item.id)">Delete</ElButton>
        </div>
    </div>
</template>

<script>
import DeleteModal from '@/components/DeleteModal';

export default {
    name: 'BudgetList',
    components: {
        DeleteModal,
    },
    data: () => ({
        dialogVisible: false,
        itemID: '',
    }),
    props: {
        list: {
            type: Object,
            default: () => ({}),
        },
    },
    methods: {
        openDialog(id) {
            this.itemID = id;
            this.dialogVisible = true;
        },
        closeModal() {
            this.dialogVisible = false;
        },
        deleteItem() {
            this.dialogVisible = false;
            this.$emit('initDelete', this.itemID);
        },
    }
}
</script>

<style scoped>
.list-item {
    display: flex;
    align-items: center;
    padding: 10px 15px;
}

.budget-value {
    font-weight: bold;
    margin-left: auto;
    margin-right: 20px;
}

.item-green {
    color: green;
}

.item-red {
    color: red;
}
</style>