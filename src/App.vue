<template>
  <h1 class="animate__heartBeat">Social network</h1>
  <div class="sort">
    <div class="sort-name">Sort by</div>
    <select v-model="selected" @change="sortFunction">
      <option>By name</option>
      <option>By text</option>
    </select>
  </div>
  <form-input :post="post" @createPost="createPost" @getPost="getPost" />
  <div v-if="preloader" class="preloader">Waiting for a new posts...</div>
  <postlist :post="post" @deletePost="deletePost" />
</template>

<script>
import FormInput from "@/components/formInput.vue";
import Postlist from "@/components/postlist.vue";

export default {
  name: "App",
  components: { Postlist, FormInput },
  data: () => ({
    post: [],
    textarea: "",
    preloader: false,
    filterText: "",
    selected: "By name",
  }),

  methods: {
    createPost(newObj) {
      this.post.push(newObj);
      this.name = "";
      this.body = "";
    },

    deletePost(index) {
      this.post.splice(index, 1);
    },
    async getPost() {
      this.preloader = true;
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/posts?_limit=6"
      );
      const data = await response.json();
      setTimeout(() => {
        data.forEach((el) => {
          const getNewObj = {
            id: el.id,
            name: el.title,
            body: el.body,
            avatar: `https://avatars.dicebear.com/api/male/${Date.now()}.svg`,
            date: new Date(),
          };
          this.post.push(getNewObj);
          this.preloader = false;
        });
      }, 2000);
    },
    sortFunction() {
      if (this.selected == "By name") {
        this.post.sort((a, b) => {
          return a.name.localeCompare(b.name);
        });
      }
      if (this.selected == "By text") {
        this.post.sort((a, b) => {
          return a.body.localeCompare(b.body);
        });
      }
    },
  },
};
</script>

<style>
body {
  background-color: #f8f8f8;
  padding: 15px;
}
h1 {
  text-align: center;
}

.preloader {
  color: darkred;
  font-weight: 700;
  font-size: 24px;
  text-align: center;
}

select {
  font: inherit;
  letter-spacing: inherit;
  word-spacing: inherit;
  border: 0.1em solid gray;
  padding: 0 0.2em;
  width: 100px;
  text-align: center;
}

.sort {
  display: flex;
  justify-content: flex-end;
}
.sort-name {
  margin-right: 5px;
  align-self: center;
}
</style>
