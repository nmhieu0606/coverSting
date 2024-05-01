<template>
    <div>
        <!-- Modal toggle -->
        <div class="relative mx-auto">
            <form class="max-w-sm mx-auto absolute right-0">
                <label for="message" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your
                    message</label>
                <textarea v-on:change="test" v-model="chuoi" id="message" rows="4"
                    class=" p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"></textarea>

                <label for="message" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your
                    message</label>
                <textarea @click="copyPixCodeClick" v-model="chuoi2" id="message" rows="4"
                    class=" p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"></textarea>
            </form>
        </div>
    </div>
</template>
<script setup>
    import Swal, {
        SweetAlertOptions
    } from "sweetalert2";
    import "sweetalert2/dist/sweetalert2.css";
    const chuoi = ref("");
    const chuoi2 = ref("");
    const test = () => {
        console.log(chuoi.value);

        chuoi2.value = toNonAccentVietnamese(chuoi.value);
    };

    const copyPixCodeClick = () => {
        navigator.clipboard.writeText(chuoi2.value);
        const Toast = Swal.mixin({
            toast: true,
            position: "top-center",
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
            didOpen: (toast) => {
                toast.onmouseenter = Swal.stopTimer;
                toast.onmouseleave = Swal.resumeTimer;
            }
        });
        Toast.fire({
            icon: "success",
            title: "Đã copy"
        });
    };

    function toNonAccentVietnamese(str) {
        str = str.replace(/A|Á|À|Ả|Ã|Ạ|Â|Ấ|Ầ|Ẫ|Ậ|Ẩ|Ă|Ắ|Ẳ|Ằ|Ẵ|Ặ/g, "A");
        str = str.replace(/à|a|á|ạ|ả|ã|â|ầ|ấ|ậ|ẩ|ẫ|ă|ằ|ắ|ặ|ẳ|ẵ/g, "a");
        str = str.replace(/E|É|È|Ẽ|Ẹ|Ê|Ế|Ề|Ễ|Ệ/, "E");
        str = str.replace(/è|é|ẹ|ẻ|ẽ|ê|ề|ế|ệ|ể|ễ/g, "e");
        str = str.replace(/I|Í|Ì|Ĩ|Ị/g, "I");
        str = str.replace(/ì|í|ị|ỉ|ĩ/g, "i");
        str = str.replace(/O|Ó|Ò|Ỏ|Õ|Ọ|Ô|Ố|Ồ|Ỗ|Ộ|Ơ|Ớ|Ờ|Ỡ|Ở|Ợ/g, "O");
        str = str.replace(/ò|ó|ọ|ỏ|õ|ô|ồ|ố|ộ|ổ|ỗ|ơ|ờ|ớ|ợ|ở|ỡ/g, "o");
        str = str.replace(/U|Ú|Ù|Ũ|Ụ|Ư|Ứ|Ừ|Ữ|Ự/g, "U");
        str = str.replace(/ù|ú|ụ|ủ|ũ|ư|ừ|ứ|ự|ử|ữ/g, "u");
        str = str.replace(/Y|Ý|Ỳ|Ỹ|Ỵ/g, "Y");
        str = str.replace(/ỳ|ý|ỵ|ỷ|ỹ/g, "y");
        str = str.replace(/Đ/g, "D");
        str = str.replace(/đ/g, "d");
        // Some system encode vietnamese combining accent as individual utf-8 characters
        str = str.replace(/\u0300|\u0301|\u0303|\u0309|\u0323/g, ""); // Huyền sắc hỏi ngã nặng
        str = str.replace(/\u02C6|\u0306|\u031B/g, ""); // Â, Ê, Ă, Ơ, Ư
        return str;
    }
</script>
