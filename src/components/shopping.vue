<template>
  <div class="wrap">
    <h1>쇼핑 목록</h1>
    
    <!-- 새 항목 추가 -->
    <input class="main-input" v-model="newItem" placeholder="새로운 항목 입력" />
    <button class="add-button" @click="addItem">추가</button>

    <!-- 조건부 렌더링 -->
    <p v-if="shoppingList.length > 0" class="main-text">
      현재 {{ shoppingList.length }}개의 물품이 있습니다:
    </p>
    <p v-else class="main-text">현재 쇼핑 목록이 비어 있습니다.</p>

    <!-- 리스트 렌더링 -->
    <ul class="Ul">
      <li v-for="(item, index) in shoppingList" :key="index" class='list-wrap'>
          <input
            type="checkbox"
            :checked="item.isCompleted"
            @change="toggleComplete(index)"
            class='checked-box'
          />
        <!-- 완료/미완료 표시 -->
        <template v-if="item.isEditing" >
            <input
              v-model="item.text"
              placeholder="수정할 내용 입력"
            />
            <button @click="finishEditing(index)">확인</button>
            <button @click="cancelEditing(index)">취소</button>
          </template>
          <template v-else>
            
            {{ item.text }}
            <span v-if="item.isCompleted">(완료)</span>
            <span v-else>(미완료)</span>
            <button @click="removeItem(index)">삭제</button>
            <button @click="startEditing(index)">수정</button>
      
        </template>

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      shoppingList: [], // 쇼핑 목록 배열
      newItem: "", // 새로 추가할 항목
    };
  },
  methods: {
    // 항목 추가
    addItem() {
      if (this.newItem.trim() !== "") {
        this.shoppingList.push({
          text: this.newItem.trim(),
          isCompleted: false, // 완료 상태
          isEditing: false, // 수정 상태
        });
        this.newItem = ""; // 입력 필드 초기화
      }
    },
    // 항목 삭제
    removeItem(index) {
      
      if(confirm('정말 삭제하시겠습니까?')){
        this.shoppingList.splice(index, 1) // 지정한 인덱스에서 항목 삭제
      }
    },
    // 완료 상태 토글
    toggleComplete(index) {
      this.shoppingList[index].isCompleted = !this.shoppingList[index].isCompleted;
    },
    
    // 수정 모드 시작
    startEditing(index) {
      this.shoppingList.forEach((item, i) => {
        item.isEditing = i === index; // 클릭된 항목만 수정 모드로 설정
      });
    },
    // 수정 모드 종료 (저장)
    finishEditing(index) {
      this.shoppingList[index].isEditing = false; // 수정 모드 종료
    },
    // 수정 취소
    cancelEditing(index) {
      this.shoppingList[index].isEditing = false; // 수정 모드 종료
    },
  },
};
</script>

<style scoped>
.Ul {
  list-style-type: none;
  width:42vw;
  height:100vh;
  border: 1px solid;
  border:none;
  box-shadow:0px 0px 3px 3px whitesmoke;
  overflow:auto;
  border-radius:15px;
}
.wrap{
  display: flex;
  flex-direction: column;
  width:100vw;
  height:100vh;
  align-items: center;
}

.main-input{
  width:25vw;
  height:6vh;
  padding-left:20px
}
.add-button{
  width:90px;
  height:35px;
  margin-top:20px;
}
.main-text{
  font-size:25px;
}
.checked-box{
  width:34px;
  height:35px;
  margin-top:10px;
  margin-right:100px;
}
.list-wrap{
  width:500px;
  height:60px;
  border: 1px solid;
  margin:30px;
  }


</style>
