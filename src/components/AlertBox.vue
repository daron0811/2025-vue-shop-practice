<template>
    <div class="toast show align-items-center text-white bg-success border-0" v-if="msg">
        <div class="d-flex">
            <div class="toast-body"><span v-html="msg"></span></div>
            <button type="button" class="btn-close btn-close-white me-2 m-auto" @click="msg = ''"></button>
        </div>
    </div>

    <div class="toast show align-items-center text-white bg-warning border-0" v-if="warnMsg">
        <div class="d-flex">
            <div class="toast-body"><span v-html="warnMsg"></span></div>
            <button type="button" class="btn-close btn-close-white me-2 m-auto" @click="warnMsg = ''"></button>
        </div>
    </div>
</template>

<script setup>
import { inject, watch } from 'vue'

// 定義inject的方法，可以變數或函式功能
const msg = inject('showAlert', '') // 第二個參數是沒有帶入參數時的預設值
const warnMsg = inject('showWarnAlert', '')


//// 監聽變化
if (msg) {
    watch(msg, (newVal, oldVal) => {
        if (newVal) {
            // 這裡可以做動畫 / 自動消失 / 呼叫 API ...
            setTimeout(() => {
                msg.value = '' // 3 秒後自動清掉
            }, 3000)
        }
    })
}

if (warnMsg) {
    watch(warnMsg, (newVal, oldVal) => {
        if (newVal) {
            // 這裡可以做動畫 / 自動消失 / 呼叫 API ...
            setTimeout(() => {
                warnMsg.value = '' // 3 秒後自動清掉
            }, 3000)
        }
    })
}

</script>