<template>
    <form @submit.prevent="updateUsers()">
        <a-card title="Cập nhật tài khoản" style="width: 100%;">
            <div class="row mb-3">
                <div class="col-12 col-sm-4">
                    <div class="row">
                        <div class="col-12 d-flex justify-content-center mb-3">
                            <a-avatar shape="square" :size="200">
                                <template #icon>
                                    <img alt="" src="../../../imgs/bn.jpg"/>
                                </template>
                            </a-avatar>
                        </div>

                    </div>

                    <div class="col-12 d-flex justify-content-center">
                        <a-button type="primary">
                            <PlusOutlined class="me-2"/>
                            <span>
                                Chọn ảnh
                            </span>
                        </a-button>
                    </div>

                </div>

                <div class="col-12 col-sm-8">
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span 
                                :class="{
                                    'text-danger': errors.status_id
                                }"
                                >
                                    Tình trạng:
                                </span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-6">
                            <a-select
                                show-search
                                placeholder="Tình trạng"
                                style="width: 100%"
                                :options="users_status"
                                :filter-option="filterOption"
                                allow-clear
                                v-model:value="status_id"
                                :class="{
                                    'select-danger': errors.status_id
                                }"
                            ></a-select>
                            <div class="w-100"></div>
                            <small v-if="errors.status_id" class="text-danger">{{ errors.status_id[0] }}</small>
                        </div>
                    </div>

                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span
                                :class="{
                                    'text-danger': errors.uername
                                }"
                                >Tên tài khoản:</span>
                            </label>
                        </div>
                        <div class="col-12 col-sm-6">
                            <a-input 
                                placeholder="Tên tài khoản" 
                                allow-clear 
                                v-model:value="uername"
                                :class="{
                                    'input-danger': errors.uername
                                }"
                            />

                            <div class="w-100"></div>
                            <small v-if="errors.uername" class="text-danger">{{ errors.uername[0] }}</small>
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                        <label>
                            <span class="text-danger me-1">*</span>
                            <span
                            :class="{
                                'text-danger': errors.name
                            }"
                            >Họ và Tên:
                        </span>
                        </label>
                        </div>
            
                        <div class="col-12 col-sm-6">
                        <a-input
                            placeholder="Họ và Tên"
                            allow-clear
                            v-model:value="name"
                            :class="{
                                'input-danger': errors.name
                            }"
                        />
                        <div class="w-100"></div>
                        <small v-if="errors.name" class="text-danger">{{ errors.name[0] }}</small>
                        </div>
                    </div>
            
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                        <label>
                            <span class="text-danger me-1">*</span>
                            <span
                            :class="{
                                'text-danger': errors.name
                            }"
                            >Email:
                        </span>
                        </label>
                        </div>
            
                        <div class="col-12 col-sm-6">
                        <a-input
                            placeholder="Email"
                            allow-clear
                            v-model:value="email"
                            :class="{
                                'input-danger': errors.email
                            }"
                        />
                        <div class="w-100"></div>
                        <small v-if="errors.email" class="text-danger">{{ errors.email[0] }}</small>
                        </div>
                    </div>
            
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                        <label>
                            <span class="text-danger me-1">*</span>
                            <span
                            :class="{
                                'text-danger': errors.deparment_id
                            }"
                            >
                                Phòng ban:
                            </span>
                        </label>
                        </div>
                        <div class="col-12 col-sm-6">
                            <a-select
                            show-search
                            placeholder="Phòng ban"
                            style="width: 100%"
                            :options="departments"
                            :filter-option="filterOption"
                            allow-clear
                            v-model:value="deparment_id"
                            :class="{
                                'select-danger': errors.deparment_id
                            }"
                            ></a-select>
                            <div class="w-100"></div>
                            <small v-if="errors.deparment_id" class="text-danger">{{ errors.deparment_id[0] }}</small>
                        </div>
                    </div>





                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">

                        </div>
            
                        <div class="col-12 col-sm-6">
                            <a-checkbox v-model:checked="change_password">
                                Đổi mật khẩu
                            </a-checkbox>
                        </div>
                    </div>



                    
                    <div class="row mb-3" v-if="change_password==true">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                        <label>
                            <span class="text-danger me-1">*</span>
                            <span>
                                Mật khẩu:
                            </span>
                        </label>
                        </div>
            
                        <div class="col-12 col-sm-6">
                            <a-input-password
                                placeholder="Mật khẩu"
                                allow-clear
                                v-model:value="password"
                            />
                        </div>
                    </div>






                    <div class="row mb-3" v-if="change_password==true">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                        <label>
                            <span class="text-danger me-1">*</span>
                            <span>
                            Xác nhận mật khẩu:
                        </span>
                        </label>
                        </div>
            
                        <div class="col-12 col-sm-6">
                        <a-input-password
                            placeholder="Xác nhận mật khẩu"
                            allow-clear
                            v-model:value="password_confirmation"
                        />
                        </div>
                    </div>




                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                        <label>
                            <span>
                            Lần đăng nhập gần đây:
                        </span>
                        </label>
                        </div>
                        <div class="col-12 col-sm-6">
                            <span>
                                {{ login_at }}
                            </span>
                        </div>
                    </div>

                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                        <label>
                            <span>
                            Lần đổi mật khẩu gần đây:
                        </span>
                        </label>
                        </div>
                        <div class="col-12 col-sm-6">
                            <span>
                                {{ change_password_at }}
                            </span>
                        </div>
                    </div>







                </div>
            </div>
            <div class="row">
                <div class="col-12 d-grid d-sm-flex justify-content-sm-end mx-auto">
                    <a-button class="me-0 me-sm-2 mb-3 mb-sm-0">
                        <router-link :to="{name: 'admin-users'}">
                            <span> Huỷ</span>
                        </router-link>
                    </a-button>
                    <a-button type="primary" html-type="submit">
                        <span> Lưu</span>
                    </a-button>
                </div>
            </div>
        </a-card>
    </form>
</template>

<script>
import {defineComponent , ref, reactive, toRefs} from 'vue'
import { useMenu } from "../../../stores/use-menu.js";
import { useRouter } from 'vue-router';
import { useRoute } from 'vue-router';
import { PlusOutlined } from '@ant-design/icons-vue';
import {message} from 'ant-design-vue';


export default defineComponent ({
    components: {
        PlusOutlined,
    },
    setup() {
        useMenu().onSelectedKeys(["admin-users"]);


        const router = useRouter();
        const route = useRoute();
        const users_status = ref([]);
        const departments = ref([]);
        const users = reactive({
            uername: "",
            name: "",
            email: "",
            password: "",
            password_confirmation: "",
            deparment_id: [],
            status_id: [],
            change_password: false,
            login_at:"",
            change_password_at: "",
        });

        const errors = ref({});

       const getUsersEdit = () => {
        // console.log(`users dang truy xuat co id la: ${route.params.id}`);
        axios.get(`http://127.0.0.1:8000/api/users/${route.params.id}/edit`)
        .then((response) => {
            users.uername =response.data.users.uername;
            users.name =response.data.users.name;
            users.email =response.data.users.email;
            users.status_id =response.data.users.status_id;
            users.deparment_id =response.data.users.deparment_id;


            response.data.users.login_at ? users.login_at =response.data.users.login_at : users.login_at = "chưa có lượt đăng nhập";
            response.data.users.change_password_at ? users.change_password_at =response.data.users.change_password_at : users.change_password_at = "chưa có lượt đổi mật khẩu";
    

            users_status.value = response.data.users_status;
            departments.value = response.data.departments;
        })
        .catch((error) => {
            console.log(error);
        })
       };



       const updateUsers = () => {
        axios.put(`http://127.0.0.1:8000/api/users/${route.params.id}`, users)
        .then((response) => {
            console.log(response);
        })
        .catch((error) => {
            errors.value = error.response.data.errors;
        });
       }






        const filterOption = (input, option) => {
            return option.label.toLowerCase().indexOf(input.toLowerCase()) >= 0;
        };

        getUsersEdit();

        return {
            users_status,
            departments,
            ...toRefs(users),
            filterOption,
            errors,
            updateUsers
        }
    }
})
</script>
<style scoped>
    .select-danger {
        border: 1px solid red;
        border-radius: 7px;
    }
    .input-danger {
        border: 1px solid red;
        border-radius: 7px;
    }
</style>