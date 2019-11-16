<template>
    <div class="total-value" :class="balanceColor">
        Balance: {{ total }}
    </div>
</template>

<script>
export default {
    name: 'TotalBalance',
    props: {
        total: {
            type: Number,
            default: 0,
        }
    },
    computed: {
        balanceColor() {
            return {
                "balance-red": this.total < 0,
                "balance-black": this.total === 0,
                "balance-green": this.total > 0,
            }
        }
    }
}
</script>

<style scoped>
.total-value {
    font-size: 26px;
    text-transform: uppercase;
    padding: 20px;
    text-align: center;
}

.balance-red {
    color: red;
}

.balance-black {
    color: black;
}

.balance-green {
    color: green;
}
</style>