<template>
  <form @click.prevent class="form">
    <label>Post Name</label>
    <input type="text" placeholder="My life" v-model="name" />
    <label>Post text</label>
    <input
      type="text"
      placeholder="My name is Jack, and I'm developer"
      v-model="body"
    />
    <div v-show="error" class="error">
      The number of characters of Post Name or Post text cannot be equal to zero
    </div>

    <button type="submit" @click="createPost" class="create-btn">
      Create post
    </button>
    <button @click="getPost" class="create-btn" style="margin-top: 10px">
      Get posts from API
    </button>
  </form>
</template>

<script>
export default {
  name: "formInput",
  props: {
    post: {
      type: Object,
    },
  },
  data: () => ({
    name: "",
    body: "",
    error: false,
  }),
  methods: {
    createPost() {
      if (this.name.length === 0 || this.body.length === 0) {
        return (this.error = true);
      }
      let newObj = {
        id: Date.now(),
        name: this.name,
        body: this.body,
        avatar: `https://avatars.dicebear.com/api/male/${Date.now()}.svg`,
        date: new Date(),
      };
      this.$emit("createPost", newObj);
      this.name = "";
      this.body = "";
      this.error = false;
    },
    getPost() {
      this.$emit("getPost");
    },
  },
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  padding: 20px;
}
input[type="text"] {
  width: 100%;
  padding: 12px 20px;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: #f8f8f8;
  resize: vertical;
  margin-top: 10px;
  margin-bottom: 20px;
}

.create-btn {
  font-weight: 700;
  color: white;
  text-decoration: none;
  padding: 0.8em 1em calc(0.8em + 3px);
  border-radius: 3px;
  background: rgb(64, 199, 129);
  box-shadow: 0 -3px rgb(53, 167, 110) inset;
  transition: 0.2s;
  cursor: pointer;
  border: none;
  width: 200px;
  align-self: center;
}
.create-btn:hover {
  background: rgb(53, 167, 110);
}
.create-btn:active {
  background: rgb(33, 147, 90);
  box-shadow: 0 3px rgb(33, 147, 90) inset;
}

.error {
  text-align: center;
  color: darkred;
  font-weight: 700;
  font-size: 20px;
  display: inline-block;
  margin-bottom: 20px;
}
</style>
