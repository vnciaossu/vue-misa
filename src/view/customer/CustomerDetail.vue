<template>
    <div >
         <div id="dlgCustomerDetail" class="dialog " :class="{'dialog-hide':!isShow}" >
        <div class="model"></div>
        <div class="dialog-content">
            <div class="dialog-header">
                <div class="dialog-title">THÔNG TIN KHÁCH HÀNG</div>
                <div class="dialog-close-button" @click="btnCloseOnClick()">&#x2715;</div>
            </div>
            <div class="dialog-body">
                <div class="m-row">
                    <div class="m-col">
                        <label>Mã khách hàng</label>
                        <input id="txtCustomerCode" type="text" v-bind:value="customer.CustomerCode" v-on:input="customer.CustomerCode = $event.target.value"/>
                    </div>
                    <div class="m-col">
                        <label>Họ và tên</label>
                        <input id="txtFullName" type="text" v-bind:value="customer.FullName" v-on:input="customer.FullName = $event.target.value"/>
                    </div>
                </div>
                <div class="m-row">
                    <div class="m-col">
                        <label>Nhóm khách hàng</label>
                        <select id="cbCustomerGroup" v-bind:value="customer.CustomerGroupId" v-on:input="customer.CustomerGroupId = $event.target.value">
                            <option value="0cb5da7c-59cd-4953-b17e-c9adc9161663">Nhóm khách hàng MISA</option>
                            <option value="19165ed7-212e-21c4-0428-030d4265475f">Khách VIP</option>
                            <option value="3631011e-4559-4ad8-b0ad-cb989f2177da">Khách vãng lai</option>
                            <option value="7a0b757e-41eb-4df6-c6f8-494a84b910f4">Khách thường</option>
                        </select>
                    </div>
                </div>
                <div class="m-row">
                    <div class="m-col">
                        <label>Giới tính</label>
                        <select id='cbGender'  v-bind:value="customer.Gender" v-on:input="customer.Gender = $event.target.value">
                            <option value="1">Nam</option>
                            <option value="0" >Nữ</option>
                            <option value="2">Không xác định</option>
                        </select>
                    </div>
                    <div class="m-col">
                        <label>Ngày sinh</label>
                        <input id="dtDateOfBirth" type="date" v-bind:value="fomatBirthday(customer.DateOfBirth)" v-on:input="customer.DateOfBirth = $event.target.value"/>
                    </div>
                </div>
                <div class="m-row">
                    <div class="m-col">
                        <label>Số điện thoại</label>
                        <input id="txtPhoneNumber" type="text" v-bind:value="customer.PhoneNumber" v-on:input="customer.PhoneNumber = $event.target.value"/>
                    </div>
                    <div class="m-col">
                        <label>Email</label>
                        <input id="txtEmail" type="text" v-bind:value="customer.Email" v-on:input="customer.Email = $event.target.value" />
                    </div>
                </div>
            </div>
            <div class="dialog-footer">
                <button id="btnSave" class="btn-default" @click="btnSaveOnClick()">Lưu</button>
            </div>
        </div>
    </div>

    </div>

</template>
<script>
import axios from 'axios';
export default {
    methods:{
        btnCloseOnClick(){
            this.$emit("hideDialog" );
            document.getElementById("txtCustomerCode").value = "";
        },
        fomatBirthday(cusbirthday){
             if(cusbirthday == null){
                 return 0;
            }
            return cusbirthday.substring(0,10);
        },
        btnSaveOnClick(){
            if(this.formMode == "add"){
                axios.post('http://api.manhnv.net/api/customers', this.customer)
                 .then((res) => {
                    console.log(res);
                    console.log(this.customer);
                    alert("Thêm thành công");
                    this.$emit("hideDialog" );
                     this.$emit("loadData" );
                })
                .catch((res) => {
                    console.log(this.customer);
                    console.log(res);
                })
            }else{
                axios.put("http://api.manhnv.net/api/customers/" + this.customer.CustomerId, this.customer)
                .then((res) => {
                    console.log(res);
                    this.$emit("hideDialog" );
                    this.$emit("loadData" );
                })
                .catch((res) => {
                    console.log(res);
                })
            }
        }, 
    },
    props:{
        isShow : {type: Boolean, default: false},
        customer: {type: Object, default: null},
        formMode: {type: String, default: "add"}
        },
    created(){
    }
}
</script>