<template>
    <ElDialog
        title="Tips"
        :visible.sync="dialogVisible"
        width="30%"
        :show-close="false"
        >
        <span>This is a message</span>
        <span slot="footer" class="dialog-footer">
            <ElButton @click="onClickClose">Cancel</ElButton>
            <ElButton type="primary" @click="onClickDelete">Confirm</ElButton>
        </span>
    </ElDialog>
</template>

<script>
export default {
    name: 'DeleteModal',
    props: {
        dialogVisible: {
            type: Boolean,
            default: false,
        }
    },
    methods: {
        onClickDelete() {
            this.$emit('initDelete', this.itemID);
        },
        onClickClose() {
            this.$emit('closed');
        }
    }
}
</script>

<style scoped>

</style>