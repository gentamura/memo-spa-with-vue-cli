<template>
  <div class="container">
    <div class="container-left">
      <ul class="list">
        <li
          v-for="memo in memos"
          :key="memo.id"
          @dblclick="edit(memo)"
        >
          {{ memo.text | title }}
        </li>
      </ul>

      <form @submit.prevent="create" class="add-list-item">
        <button>+</button>
      </form>
    </div>

    <div class="container-right" v-if="memo">
      <textarea v-model="memo.text" />

      <div>
        <button @click="update(memo.id)">Update</button>
        <button @click="remove(memo.id)">Remove</button>
      </div>
    </div>
  </div>
</template>

<script>
const storageKey = 'memo-spa-with-vue-cli:memos';

const initMemos = () => {
  const storage = localStorage.getItem(storageKey);

  return storage ? JSON.parse(storage) : [];
};

const saveMemos = (memos) => {
  localStorage.setItem(storageKey, JSON.stringify(memos));
};

const generateId = (memos) => {
  if (memos.length === 0) return 1;

  let { id } = memos[memos.length - 1];
  return ++id;
};

export default {
  name: 'Memos',
  data: function() {
    return {
      memos: initMemos(),
      memo: null,
    };
  },
  filters: {
    title: function (text) {
      return text.split(/\r?\n/)[0];
    }
  },
  methods: {
    create: function() {
      const id = generateId(this.memos);

      const memo = {
        id,
        text: '新規メモ',
      };

      this.memos.push(memo);

      saveMemos(this.memos);

      this.edit(memo);
    },
    edit: function(memo) {
      this.memo = memo;
    },
    update: function() {
      saveMemos(this.memos);

      this.memo = null;
    },
    remove: function(id) {
      this.memos = this.memos.filter(memo => memo.id !== id);

      saveMemos(this.memos);

      this.memo = null;
    },
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  width: 400px;
  display: flex;
}
.container > div {
  flex: 1;
}

.list {
  list-style: none;
  padding-left: 0;
  text-align: left;
}

.add-list-item {
  text-align: left;
}

.container-right > textarea {
  width: 100%;
  min-height: 180px;
}
</style>

