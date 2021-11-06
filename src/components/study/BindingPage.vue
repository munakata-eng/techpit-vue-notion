<template>
  <div class="binding-page">
    <h2>学習1：双方向バインディング</h2>

    <!-- 従来のJavaScript -->
    <h3><span class="badge badge-secondary">JavaScript</span></h3>
    <input class="form-control" id="name" />
    <span id="text">入力された名前はです</span>
    <br />
    <br />

    <!-- Vue.js -->
    <h3><span class="badge badge-secondary">Vue.js</span></h3>
    <input class="form-control" v-model="name">
    <span>入力された名前は{{name}}です</span>
  </div>
</template>

<script>
// 従来のJavaScript
window.onload = function() {
  const nameInput = document.getElementById('name');
  nameInput.oninput = function() {
    const name = nameInput.value;
    const text = document.getElementById('text');
    text.innerHTML = '入力された名前は' +  name + 'です';
  };
}
export default {
  data() { 
    return {
      name : ''
    }
  }
}
</script>

<style scoped>
.binding-page {
  padding: 20px;
}
</style>
