<template>
  <div>
    <h1>쇼핑 목록</h1>
    
    <!-- 새 항목 추가 -->
    <input v-model="newItem" placeholder="새로운 항목 입력" />
    <button v-if="'inVisible'" @click="addItem">추가</button>

    <!-- 조건부 렌더링 -->
    <p v-if="shoppingList.length > 0">현재 {{ shoppingList.length }}개의 물품이 있습니다:</p> 
    <!-- 쇼핑 리스트의 길이를 개수로 표현 -->
    <p v-else>현재 쇼핑 목록이 비어 있습니다.</p>
    <!-- 리스트가 비어있을 떄 이 p 태그 보이기 -->

    <!-- 리스트 렌더링 -->
    <ul>
      <li v-for="(item, index) in shoppingList" :key="index">
        {{ item }}
        <!-- 이벤트 처리 -->
        <button @click="removeItem(index)">삭제</button>
        <button v-if="inVisible" @click="visibleSetItem">취소</button>
        <button v-else="inVisible" @click="visibleSetItem">수정</button>
        <input v-if="inVisible" v-model="setItems" placeholder="수정 할 내용 입력">
        <button v-if="inVisible" @click="setItem(index)">확인</button>

        <button @click="visibleSetItemRead(index)">읽기</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() { // data의 변수를 지정해서 this를 사용해 접근함
    return {
      shoppingList: [], // 쇼핑 목록 배열
      newItem: "", // 새로 추가할 항목
      inVisible: false,
      setItems:''
    };
  },
  methods: {
    // 항목 추가
    addItem() {
      if (this.newItem.trim() !== "") {
        this.shoppingList.push(this.newItem.trim());
        this.newItem = ""; // 입력 필드 초기화
      }
    },
    // 항목 삭제
    removeItem(index) {
      if(confirm('정말 지우시겠습니까?')){
        this.shoppingList.splice(index, 1);
      }
      // 지정한 인덱스에서 항목 삭제
      // array.splice(start, deleteCount, ...items) splice는 이러한 형식임
      // 시작인덱스, 삭제할 갯수, 지우고 난뒤에 넣을 값

    },
    visibleSetItem(){
      this.inVisible = !this.inVisible;
    },
    visibleSetItemRead(index){
      alert(this.shoppingList[index])
    },

    setItem(index){
      if (this.setItems.trim() !== ""){
        this.shoppingList.splice(index,1,this.setItems);
        this.setItems ='';
        this.inVisible = false;
      }

    }
  },
};
</script>