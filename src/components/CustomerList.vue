<template>
    <div>
        <div v-if="!showView">
            <input v-model="searchText" type="text" class="form-control" placeholder="Search value...">
            <small v-if="searchText"> Şu an <b>{{searchText}}</b> için arama yapıyorsunuz.</small>
            <table v-if="filterCustomers.length > 0" class="table table-striped">
                <thead>
                    <th>First Name</th>
                    <th>Last Name</th>
                    <th>Email</th>
                    <th>View</th>
                </thead>
                <tbody>
                    <tr v-for="item in filterCustomers.slice((this.activePage * 4) - 4,this.activePage * 4)" :key="item.id">
                        <td> {{item.firstName}} </td>
                        <td> {{item.lastName}} </td>
                        <td> {{item.email}} </td>
                        <td>
                            <button @click="getCustomerView(item.id)" class="btn btn-outline-dark">VIEW</button>
                        </td>
                    </tr>
                </tbody>
            </table>
            <h3 v-else align="center">Arama kriterlerinize uygun sonuç bulunamamıştır.</h3>
            <ul class="list-group list-group-horizontal">
                <li @click="activePage = count" v-for="count in pageCount" :key="count" :class="{active : activePage === count}" class="list-group-item" style="cursor: pointer;"> {{count}} </li>
            </ul>
        </div>
        <div v-else>
            <button @click="showView = false" class="btn btn-danger" style="margin-bottom: 10px;">BACK</button>
            <ul class="list-group">
                <li class="list-group-item"> {{selectedItem.firstName}} </li>
                <li class="list-group-item"> {{selectedItem.lastName}} </li>
                <li class="list-group-item"> {{selectedItem.email}} </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        props: ["items"],
        data() {
            return {
                searchText: "",
                selectedItem: null,
                showView: false,
                activePage: 1,
            }
        },
        methods: {
            getCustomerView(id) {
                this.selectedItem = this.items.find(item => item.id === id);
                this.showView = true;
            }
        },
        computed: {
            filterCustomers() {
                return this.searchText === "" ? this.items : this.items.filter((item) =>
                    item.firstName.toLowerCase().includes(this.searchText.toLowerCase()) ||
                    item.lastName.toLowerCase().includes(this.searchText.toLowerCase()) ||
                    item.email.toLowerCase().includes(this.searchText.toLowerCase())
                )
            },
            pageCount() {
                return Math.ceil(this.filterCustomers.length / 4);
            }
        } 
    }
</script>

<style></style>