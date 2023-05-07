<script setup>
import { ref } from 'vue';

const barClass = ref('searchBar')
const spanH = ref(60)
const spanW = ref(400)
const show = () => {
    barClass.value = 'searchBar-show'
}   

const hide = () => {
    barClass.value = 'searchBar'
}
</script>

<template>  
    <div class="cont" :style="{
    '--my-height': spanH +'px',
    '--my-width': spanW +'px',
    '--my-height-d2': (spanH / 2) +'px',
    '--my-height-d4': (spanH / 4) +'px',
    '--my-width-d32': (spanW / 3 * 2) +'px',
    '--my-height-d43': (spanH / 4 * 3) +'px'
}">
        <div :class="barClass">
        <div class="icon"><el-icon><Search /></el-icon></div>
        <div class="textInput">
            <input type="text" placeholder="please input" @focus="show" @focusout="hide">
        </div>
    </div>
    </div>
</template> 

<style scoped>
.cont {
    width: var(--my-width);
    height: var(--my-height);
}

.searchBar {
    position: relative;
    margin: 10px 0;
    width: var(--my-height);
    height: var(--my-height);
    border-radius: var(--my-height);
    background-color: #010f01;
    box-shadow: 0 10px 10px rgba(13, 69, 120, 0.6);
    overflow: hidden;

    transition: 0.5s;
}

.searchBar:hover {
    width: 100%;
    animation: stretch 0.6s;
}
@keyframes stretch {
  0% {
    width: var(--my-height);
  }
  75% {
    width: 101%;
  }
  100% {
    width: 100%;
  }
}

.searchBar-show {
    position: relative;
    margin: 10px 0;
    width: 100%;
    height: var(--my-height);
    border-radius: var(--my-height);
    background-color: #010f01;
    box-shadow: 0 10px 10px rgba(13, 69, 120, 0.6);
    transition: 0.5s;
}

.icon {
    position: absolute;
    color: dodgerblue;
    transform: translate(15px,15px);
    font-size: var(--my-height-d2);
}

.textInput {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    width: var(--my-width-d32);
    height: var(--my-height-d43);
    border-radius: 12px;
    background-color: #010f01;
    top: 7px;
    left: var(--my-height);
    overflow: hidden;
}
.textInput input{
    color: aliceblue;
    width: 100%;
    height: 100%;
    font-size: 3vh;
    border-radius: 10px;
    border: none;
    background-color: #010f01;
}

</style>