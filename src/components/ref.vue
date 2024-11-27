<script setup>
import { ref } from 'vue';

const count = ref(0);
const increment = () =>{
    count.value += 1; 
}
const decrement = () => {
  count.value -= 1;
}
</script>

  <template >
    <div class="mom">
      <p>{{count}}</p>
      <button class="countBtn" @click="increment">+</button>
      <button class="countBtn" @click="decrement">-</button>
    </div>
  </template>

  <style>
    html,body{
      margin:0;
    }
    .mom {
      display: flex;
      flex-direction: column;
      width: 100%;
      height: 100vh;
      align-items  : center;
    }
    .countBtn{
      width:200px;
      height:50px;
      border-radius: 20px;
    }
    
  </style>