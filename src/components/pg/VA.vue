<template>
    <div class="fund-wrapper dret" id="fund">
    <div class="jet">
        <div class="content-container">
            <h1>add</h1>
            <h1>BENEFICAIRY</h1>
            <p>fund your account using the paystack api</p>
            <span class="submit-btn" style="display: inherit">
                <button style="width: 200px" @click="this.$store.commit('showBen')">View All Beneficairies</button>
            </span>
        </div>
    </div>
    <div class="form-container glee set">
        <div class="input-container">
            <div role="tablist" class="accordion" id="accordion-1" style="width: 100%;">
                <div class="accordion-item" style="border: 0;">
                    <h2 role="tab" class="accordion-header"><button data-bs-toggle="collapse" data-bs-target="#accordion-1 .item-1" aria-expanded="false" aria-controls="accordion-1 .item-1" class="accordion-button collapsed" style="background-color: #ffffff;box-shadow: -1px 5px 29px 0 rgba(0,0,0,0.07);">Choose Bank</button></h2>
                    <div role="tabpanel" data-bs-parent="#accordion-1" class="accordion-collapse collapse item-1" style="margin-top: 5%;">
                        <div class="accordion-body" v-for="bank in banks" :key="bank.name">
                            <div class="banks" type="button" @click="this.$store.commit('addCode', bank.code)">
                                <p>{{ bank.name }}</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <form @submit.prevent="this.$store.dispatch('verifyAccount', accNum)">
            <div class="input-container"><input type="text" class="form-control" v-model="accNum" placeholder="Account Number" /></div>
            <div class="submit-btn"><button>Save</button></div>
        </form>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'VA',
    data() {
        return {
            banks: [],
            accNum: ''
        }
    },
    async created() {
        await axios.get('https://backend--backendproject.herokuapp.com/payapi/account/code_list')
        .then((response) => {
            this.banks = response.data.data
            console.log(response.data)
        })
    }
}

</script>

<style>

</style>