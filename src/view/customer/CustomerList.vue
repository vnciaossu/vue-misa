<template>
    <div>
         <div class="page-title">
            <div class="page-left">Danh sách khách hàng</div>
            <div class="page-right">
                <button id="btnAdd" class="btn-default" @click="btnAddOnClick()">Thêm khách hàng</button>
            </div>
        </div>
        <div class="toolbar">
            <input type="text" class="input-search" style="width: 220px;" placeholder="Tìm kiếm theo mã, tên khách hàng" />
            <button class="btn-refresh" @click=" loadData()"></button>
            <button class="btn-delete" @click="btnDeleteOnClick(customerId)"></button>
        </div>
        <div class="grid">
            <table id="tblListCustomer" class="table" width="100%" border="0">
                <thead>
                    <tr>
                        <th>Mã khách hàng</th>
                        <th>Họ và tên</th>
                        <th>Giới tính</th>
                        <th>Ngày sinh</th>
                        <th>Nhóm khách hàng</th>
                        <th>Điện thoại</th>
                        <th>Email</th>
                        <th class="text-align-right">Số tiền nợ</th>
                        <th class="text-align-center">Đang hoạt động</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="customer in customers" :key="customer.CustomerId" @dblclick="trOnDblClick(customer.CustomerId)"
                     @click="getCustomerId(customer.CustomerId)" v-bind:class="{'customerClick':customer.CustomerId===customerClick}">
                        <td>{{customer.CustomerCode}}</td>
                        <td>{{customer.FullName}}</td>
                        <td>{{customer.GenderName}}</td>
                        <td>{{fomatBirthday(customer.DateOfBirth)}}</td>
                        <td>{{customer.CustomerGroupName}}</td>
                        <td>{{customer.PhoneNumber}}</td>
                        <td>{{customer.Email}}</td>
                        <td  class="text-align-right">1.025.000</td>
                        <td class="text-align-center"><input type="radio" checked></td>
                    </tr>
                    
                </tbody>
            </table>
        </div>
        <div class="paging">
            <div data-v-a72348a4="" class="paging-bar"><div data-v-a72348a4="" class="paging-record-info">Hiển thị <b data-v-a72348a4="">1-10/1000</b> nhân viên</div><div data-v-a72348a4="" class="paging-option"><div data-v-a72348a4="" class="btn-select-page m-btn-firstpage"></div><div data-v-a72348a4="" class="btn-select-page m-btn-prev-page"></div><div data-v-a72348a4="" class="m-btn-list-page"><button data-v-a72348a4="" class="btn-pagenumber btn-pagenumber-selected">1</button><button data-v-a72348a4="" class="btn-pagenumber">2</button><button data-v-a72348a4="" class="btn-pagenumber">3</button><button data-v-a72348a4="" class="btn-pagenumber">4</button></div><div data-v-a72348a4="" class="btn-select-page m-btn-next-page"></div><div data-v-a72348a4="" class="btn-select-page m-btn-lastpage"></div></div><div data-v-a72348a4="" class="paging-record-option"><b data-v-a72348a4="">10</b> nhân viên/trang</div></div>
        </div>  
    <CustomerDetail :isShow="isShowDialogDetail" @hideDialog="hideDialog" :customer="customerDetail" :formMode="dialogFormMode" @loadData="loadData"/>

    </div>
</template>

<script>
import CustomerDetail from './CustomerDetail.vue'
import axios from 'axios'
export default {
    components:{
        CustomerDetail,
    },
    created(){
        axios
        .get("http://api.manhnv.net/api/customers")
        .then((res)=>{
            this.customers = res.data;
        })
        .catch((res) =>{
            console.log(res);
        })
    },
    props:[],
    methods:{
        loadData(){
        axios
        .get("http://api.manhnv.net/api/customers")
        .then((res)=>{
            this.customers = res.data;
        })
        .catch((res) =>{
            console.log(res);
        })
        },
        btnAddOnClick(){       
            this.isShowDialogDetail =  true;
            this.dialogFormMode= "add";
            this.customerDetail = {};
        },
        hideDialog(){
            this.isShowDialogDetail =  false;
        },
        trOnDblClick(customerId){
            //Lay id ban ghi
            
            //Goi Api lay thong tin khac hang
            axios
            .get("http://api.manhnv.net/api/customers/"+customerId)
            .then((res)=>{
                this.customerDetail = res.data;
            })
            .catch((res) =>{
                console.log(res);
            })
            //Thuc hien bindding du lieu

            //Cap nhap trang thai
            this.dialogFormMode =  "edit"
            //Hien thi Dialog
             this.isShowDialogDetail =  true;
        },
        fomatBirthday(cusbirthday){
             if(cusbirthday == null){
                 return "Không có";
            }
            return cusbirthday.substring(0,10);
        },
        getCustomerId(customerId){
            this.customerId = customerId;
            this.customerClick = customerId;
        },
        btnDeleteOnClick(customerId){
             axios
            .delete("http://api.manhnv.net/api/customers/"+customerId)
            .then((res)=>{
               console.log(res);
               this.loadData();
            })
            .catch((res) =>{
                console.log(res);
            })
        }
        
    }, 
    data(){
        return{
            dialogFormMode: "add",
            isShowDialogDetail: false,
            customers: [],
            customerDetail: {},
            customerId: null,
            customerClick: null,
        }
    },
    watch: {

    }
}
</script>

<style scoped>
@import '../../style/main.css';
@import '../../style/page/customer.css';

.customerClick{
     background-color: #dedede;
}
</style>