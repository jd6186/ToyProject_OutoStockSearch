<template>
    <nav v-show="isLoad">
        <button @click="goHome">HOME</button>
        <button @click="goTransactionDetails">거래 내역 조회</button>
        <button @click="goSystemTradding">시스템트레이딩</button>
        <button @click="doLogout">로그아웃</button>
    </nav>
</template>

<script>
export default {
    data () {
        return {
            isLoad: false,
            userCheck: this.$session.get('userId')
        };
    },
    created () {
        if (!this.$session.get('userId')) {
            this.isLoad = false;
        } else {
            this.isLoad = true;
        }
    },

    // 거래 내역 페이지로 이동
    methods: {
        goHome () {
            this.$router.push(`/`);
        },
        goTransactionDetails () {
            this.$router.push(`/transactiondetails`);
        },
        doLogout () {
            this.$session.clear();
            this.$Axios.get(`${process.env.APIURL}/logout/`)
                .then(response => {
                    let data = response.data;
                    (data.status === 'SUCCESS') ? this.$router.push(`/login`) : alert(`${data.error}`);
                });
        },
        goSystemTradding () {
            this.$router.push(`/systemtradding`);
        }
    }
};
</script>
<style>
    nav {
        text-align: center;
    }
</style>
