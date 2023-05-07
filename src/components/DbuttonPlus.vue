<script setup>
import { ref,reactive,provide,inject } from 'vue';
const spanT = ref(100)
const spanL = ref(100)
const clickEvent = defineEmits(['click'])
const b = ref(null)
const m = ref('')



const findPOS = (event) => {
    const btnRect = b.value.getBoundingClientRect()
    let x = event.clientX - btnRect.left
    let y = event.clientY - btnRect.top
    spanL.value = x
    spanT.value = y
 
}

const clEvent = () => {
    // m.value = 'click-div'
    // setTimeout(() => {
    //     m.value = ''
    // }, 1000);
    // clickEvent('click','click')
}
</script>


<template>
    <div class="btn-div">
        <button ref="b" class="btn" :style="{
    '--my-paramX': spanL +'px',
    '--my-paramY': spanT +'px'
}" @mouseenter="findPOS" @mousemove="findPOS" @click="clEvent">
        <span>
            <slot></slot>
        </span>
        <div :class="m"></div>
    </button>
    </div>
</template>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

/* .btn-div {
    overflow: hidden;
    padding: 1000px 1000px;
    height: 100px;
    padding: 0;
} */

.btn {

    position: relative;
    
    padding: 20px 30px;
    font-size: 20px;
    font-weight: 500;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
    background-image: linear-gradient(rgb(184, 179, 221),rgb(75, 176, 216));
    color: #000;
    text-decoration: none;
    /* 字体 */
    /* font-family: 'Poppins',sans-serif; */
    border-radius: 5px;

    overflow: hidden;
    transition: .5s;
}

.btn:active {
    box-shadow: none;
}



.btn:hover {
    color: #fff;
}

.btn::before {
    content: "";
    position: absolute;
    left: var(--my-paramX);
    top: var(--my-paramY);
    transform: translate(-50%,-50%);
    width: 0;
    height: 0;
    /* background-color: #000; */
    background-image: linear-gradient(90deg, #49add4, #592ebe);
    border-radius: 50%;
    transition: width 0.5s ,height 0.5s;
}

.btn:hover::before {
    width: 400px;
    height: 400px;
}





.btn span {
    position: relative;
    z-index: 1;
}

.click-div {
    display: inline;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    position: absolute;
    /* left: 50%;
    top: 50%; */
    transform: translate(-50%,-50%);
    left: var(--my-paramX);
    top: var(--my-paramY);
    background-color: #fff;

    animation: animate 0.5s ease-out infinite;
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
        opacity: 0;
    }
}
</style>