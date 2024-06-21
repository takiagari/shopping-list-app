<template>
  <div class="shopping-list-app">
    <h1>Shopping List App</h1>
    <!-- 商品名を入力するテキストボックス -->
    <input v-model="newItem.name" placeholder="買うアイテム名" @keyup.enter="addItem" />
    <!-- 個数を入力するテキストボックス、デフォルトは1 -->
    <input v-model.number="newItem.quantity" type="number" class="num" min="1" placeholder="数量" @keyup.enter="addItem" />
    <!-- 商品を追加するボタン -->
    <button @click="addItem">Add Item</button>
    <!-- 商品のリストを表示 -->
    <ul>
      <li v-for="(item, index) in items" :key="index">
        {{ item.name }} ({{ item.quantity }})
        <!-- 商品を削除するボタン -->
        <button @click="deleteItem(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, onMounted, watch } from 'vue';

export default {
  name: 'ShoppingListApp',

  setup() {
    // 新しい商品情報（名前と個数）初期値
    const newItem = ref({ name: '', quantity: 1 });

    // 商品のリスト
    const items = ref([]);

    /**
     * 商品を追加する
     * 新しい商品が入力されている場合、商品をリストに追加し、入力フィールドをクリアする
     */
    const addItem = () => {
      if (newItem.value.name.trim() !== '' && newItem.value.quantity > 0) {
        items.value.push({ name: newItem.value.name.trim(), quantity: newItem.value.quantity });
        newItem.value = { name: '', quantity: 1 };
        saveItems();
      }
    };

    /**
     * 商品を削除する
     * 指定されたインデックスの商品をリストから削除する
     * @param {number} index - 削除する商品のインデックス
     */
    const deleteItem = (index) => {
      items.value.splice(index, 1);
      saveItems();
    };

    /**
     * 商品をローカルストレージに保存する
     * 現在の商品リストをローカルストレージに保存
     */
    const saveItems = () => {
      localStorage.setItem('items', JSON.stringify(items.value));
    };

    /**
     * ローカルストレージから商品を読み込む
     * ローカルストレージに保存されている商品リストを読み込み、itemsに設定
     */
    const loadItems = () => {
      const savedItems = localStorage.getItem('items');
      if (savedItems) {
        items.value = JSON.parse(savedItems);
      }
    };

    /**
     * コンポーネントがマウントされたときに商品を読み込む
     * ページが読み込まれた際にローカルストレージから商品を取得
     */
    onMounted(() => {
      loadItems();
    });

    /**
     * 商品のリストが変わるたびにローカルストレージに保存する
     * itemsが変更されるたびにsaveItems関数を呼び出す
     */
    watch(items, saveItems, { deep: true });

    return {
      newItem,
      items,
      addItem,
      deleteItem
    };
  }
};
</script>

<style>
.shopping-list-app {
  text-align: center;
}

input {
  margin-right: 1rem;
  font-size: 1.2rem;
  padding: .2rem;
}
.num {
  width: 3rem;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 1rem 0;
}

button {
  margin-left: 1rem;
}
</style>
