<template>
  <div class="list-wrapper">
    <ul v-for="(onepost, index) in post" :key="index" class="lists">
      <li class="list" style="align-self: center; margin-bottom: 10px">
        <img :src="onepost.avatar" style="width: 40px; height: 40px" />
      </li>
      <li class="list">
        <span style="font-weight: 700">Name post:</span> {{ onepost.name }}
      </li>
      <li class="list body">
        {{ onepost.body }}
      </li>
      <li
        class="list"
        style="
          font-style: italic;
          text-decoration: lightgrey;
          display: block;
          margin-top: 10px;
        "
      >
        {{ onepost.date }}
      </li>
      <li class="list list-btn">
        <button class="btn" @click="deletePost(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "post-list",
  props: {
    post: {
      type: Object,
    },
  },
  methods: {
    deletePost(index) {
      this.$emit("deletePost", index);
    },
  },
};
</script>

<style scoped>
.list-wrapper {
  display: flex;
  flex-wrap: wrap;
  padding: 30px;
}
.lists {
  display: flex;
  flex-direction: column;
  width: 300px;
  padding: 30px;
  background-color: lightgrey;
  border-radius: 10px;
}

.list {
  list-style-type: none;
}
.lists:not(:nth-child(3n)) {
  margin-right: 30px;
}

.btn {
  margin-left: auto;
  right: 15px;
  top: 15px;
  margin-right: auto;
  margin-left: auto;
  color: #fff;
  text-decoration: none;
  user-select: none;
  background: rgb(212, 75, 56);
  padding: 0.7em 1.5em;
  outline: none;
  border: none;
  cursor: pointer;
  border-radius: 6px;
}
.btn:hover {
  background: rgb(232, 95, 76);
}
.btn:active {
  background: rgb(152, 15, 0);
}

.list-btn {
  margin-right: auto;
  margin-left: auto;
}

.list.body {
  background-color: #f8f8f8;
  padding: 5px;
  border-radius: 5px;
}
</style>
