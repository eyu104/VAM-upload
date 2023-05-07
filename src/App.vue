<script setup>
  import Dbutton from '../src/components/Dbutton.vue'
  import DbuttonPlus from './components/DbuttonPlus.vue';
  // 引入新的按钮
  import Dsearch from './components/Dsearch.vue'
  import { ref } from 'vue';
  import { ElMessage } from 'element-plus'
  import { Check } from '@element-plus/icons-vue'
  const videoUrl = ref('')
  const audioUrl = ref('')
  const v = ref(null)
  const a = ref(null)
  const percentages = ref(0)
  const isSuccess = ref('exception')
  const pro = ref(false)
  const input = ref('')
  const msgText = ref('请输入您想合成的相关方面:')

  // 上传视频文件
const videoChange = (event) => {

  ElMessage({
                message: '上传成功',
                type: 'success',
                duration: 3*1000
              })

  const file = event.target.files[0];

  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      const fileURL = e.target.result;
      console.log(fileURL);
      videoUrl.value = fileURL
    };

    reader.readAsDataURL(file);
  }
}
// 上传音频文件
const audioChange = (event) => {
  ElMessage({
                message: '上传成功',
                type: 'success',
                duration: 3*1000
              })

  const file = event.target.files[0];

  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      const fileURL = e.target.result;
      console.log(fileURL);
      audioUrl.value = fileURL
    };

    reader.readAsDataURL(file);
  }
}



const handleFileChange = (event) => {
      // 处理文件改变事件
      const file = event.target.files[0];
      console.log(file);
    };


// 上传视频文件
const upload0 = () => {
  v.value.click()
}

// 上传音频文件
const upload1 = () => {
  a.value.click()
}

// 点击长传资源按钮，计时器模仿上传进度
const countTime = () => {
        pro.value = !pro.value
        console.log(pro.value + 'pro')
        percentages.value = 0
        isSuccess.value = 'exception'

        // 计时
        const intervalId = setInterval(() => {
        
        percentages.value = percentages.value + 1
        console.log(percentages.value)

        if (percentages.value === 100) {
          clearInterval(intervalId);
          isSuccess.value = 'success'
          setTimeout(() =>{
            pro.value = !pro.value
            ElMessage({
                message: '上传成功',
                type: 'success',
                duration: 3*1000
              })
          }, 1000);
          
        }
      }, 100); // 时间间隔为 100 毫秒
}


//点击合成，播放对应视频
const mix = () => {
  const vUrl = new URL('../src/assets/out.mp4', import.meta.url).href
  videoUrl.value = vUrl
  audioUrl.value = ''
  ElMessage({
                message: '合成成功',
                type: 'success',
                duration: 3*1000
              })
}

// 点击确认按钮
const confirm = () => {
// 点击确认后对msgtext的操作
  msgText.value =  '正在处理，请稍后...'
  setTimeout(() =>{
            msgText.value = '收到' + input.value
          }, 1000);
}

const btnTest = () => {
  console.log('测试按钮点击')
}

</script>

<template>
  <div class="main">
    <div class="show">
        <h2 style="text-align: center; color: #3678ac;">上传音频和视频</h2>
        <div class="video-div">
          <video v-if="videoUrl != ''" ref="videoPlayer" :src="videoUrl" controls></video>
          <audio v-if="audioUrl != ''" ref="audioPlayer" :src="audioUrl" controls></audio>
          <input ref="v" type="file" id="video-file" class="upload-btn" accept="video/*" @change="videoChange" @click="handleFileChange">
          <input ref="a" type="file" id="audio-file" class="upload-btn" accept="audio/*" @change="audioChange" @click="handleFileChange">
          
        </div>

        <div class="select">
          <Dbutton 
            @click="upload0"
             >
             上传视频文件
          </Dbutton>
<!--          按钮使用例子-->


          <Dbutton 
            @click="upload1"
             >
             上传音频文件
          </Dbutton>
        </div>
        <div class="up">
          <Dbutton 
            @click="countTime"
             >
             确认上传资源文件
          </Dbutton>
          <div v-show="pro" class="pro">
            <el-progress  type="circle" :percentage="percentages" :status="isSuccess">
              <el-button v-if="percentages == 100" type="success" :icon="Check" circle />
            </el-progress>
          </div>
        </div>
        <div class="chat">
          <p style="color: #3678ac; white-space: pre-line; font-size: 20px;">{{ msgText }}</p>
          <div class="msg">
            <el-input v-model="input" placeholder="Please input" clearable />
          </div>
          <div>
            <Dbutton 
            @click="confirm"
             >
             确认
          </Dbutton>
          <Dbutton 
            @click="mix"
             >
             合成
          </Dbutton>
           <DbuttonPlus @click="btnTest">按钮测试2</DbuttonPlus>
           <Dsearch />
          </div>
        </div>
    </div>
  </div>
</template>

<style scoped>
.main {
  background-color: #0fa8f9;
  min-height: 98VH;
  padding: 50px;
  font-family: "楷体","楷体_GB2312";
}

.upload-btn {
  display: none;
}
.show {
  top: 50px;
  width: 80vw;
  min-height: 80vh;
  margin: 10px auto;
  border-radius: 20px;
  background-color: white;
  box-shadow: 0 25px 50px rgba(1, 0, 0, 0.9);
  padding: 20px;
}

.video-div {
  margin: 10px 40px;
  border-radius: 20px;
}

.video-div video {
  margin-bottom: 20px;
  width: 100%;
  display: block;
}

.select {
  margin-top: 20px;
  margin-left: 50px;
}
.up{
  margin-top: 20px;
  margin-left: 50px;
}

.pro {
  margin-top: 10px;
}

.chat {
  margin-top: 20px;
  margin-left: 50px;
  white-space: pre-line;
}

.msg{
  margin: 0 0 10px 0;
}

.btn {
  font-size: large;
}
</style>
