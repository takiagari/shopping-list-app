<template>
  <div class="container mt-5 mw-800">
    <h1 class="text-center mb-4">Shopping List App</h1>
    <div class="container text-center mb-3">
      <div class="row">
        <div class="col-6">
          <!-- 商品名を入力するテキストボックス -->
          <input v-model="newItem.name" type="text" class="form-control mb-2" placeholder="買うアイテム名" @keyup.enter="addItem" />
        </div>
        <div class="col-2">
          <!-- 個数を入力するテキストボックス、デフォルトは1 -->
          <input v-model.number="newItem.quantity" type="number" class="form-control mb-2" min="1" placeholder="数量" @keyup.enter="addItem" />
        </div>
        <div class="col">
          <!-- 商品を追加するボタン -->
          <button @click="addItem" class="btn btn-primary w-100">Add Item</button>
        </div>
      </div>
    </div>
    
    <div class="container">
      <!-- 商品のリストをテーブルで表示 -->
      <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">商品名</th>
            <th scope="col">数量</th>
            <th scope="col">操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="index">
            <th scope="row">{{ index + 1 }}</th>
            <td>{{ item.name }}</td>
            <td>{{ item.quantity }}</td>
            <td>
              <button @click="deleteItem(index)" type="button" class="btn btn-secondary btn-sm">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
      
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

<style scoped>

body,
th,
td,
input,
button {
  font-family: "M PLUS 2", sans-serif;
}

ul {
  list-style: none;
  padding: 0;
}

h1 {
  font-weight: 200;
  color: #555;
}

tr th,
tr td {
  color: #666;
}

tr:hover th,
tr:hover td {
  color: #000;
  background: rgba(235, 247, 237, 0.9);
}

</style>
