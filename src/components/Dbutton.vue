<script setup>
import { ref } from 'vue';
const showSpan = ref(false)
const s = ref(null)
const b = ref(null)
const spanT = ref(0)
const spanL = ref(0)
const clickEvent = defineEmits(['click'])

const addSpan = (event) => {
    clickEvent('click','click')
    showSpan.value = true
    const btnRect = b.value.getBoundingClientRect()
    let x = event.clientX - btnRect.left
    let y = event.clientY - btnRect.top
    spanL.value = x
    spanT.value = y
    setTimeout(()=> {
        showSpan.value = false
    },300)
}
</script>

<template>
    <div class="btn-div">
        <button ref="b" @click="addSpan" >
            <slot></slot>
            <span ref="s" v-if="showSpan" :style="{left: spanL + 'px',top: spanT + 'px'}"></span>
        </button>
    </div>
</template>

<style scoped>


* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.btn-div {
    display: inline-block;
    margin-right: 10px;
}

button {
    overflow: hidden;

    /* 字体 */
    font-family: "楷体","楷体_GB2312";

    padding: 1vmin 2vmin;
    border: none;
    border-radius: 10vmin;
    /* 颜色 */
    background-image: linear-gradient(90deg, #0acffe, #495aff);
    color: #fff;
    /* 字体大小 */
    font-size: 3vmin;
    font-weight: bold;
    letter-spacing: 0.2vmin;
    cursor: pointer;
    position: relative;
}

button:hover {
    background-image: linear-gradient(90deg, #0ae2fe, #8049ff);
}

button span {
    background-color: #fff;
    border-radius: 50%;
    position: absolute;

    transform: translate(-50%, -50%);

    /* 动画速度 */
    animation: animate 2s ease-out infinite;
}
@keyframes animate {
    0% {
        width: 0;
        height: 0;
        opacity: 0.5;
    }
    100% {
        width: 200vmin;
        height: 200vmin;
        opacity: 0.5;
    }
}

</style>
