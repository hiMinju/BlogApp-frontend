<template>
  <v-container>
      <v-row align="center" justify="center">
        <v-col cols="12" lg="10">
          <h1>{{ post.title }}</h1>
          <p>{{ post.modify_dt }}, written by {{ post.owner }}</p>
        </v-col>
      </v-row>
      <v-row align="start" justify="center">
        <v-col sm="8" lg="7">
          <v-card class="pa-2" outlined tile>
            <p style="white-space: pre-wrap;"> {{ post.content }} </p>
            <div>
              <strong>TAGS:</strong>
              <v-chip class="ma-2" color="defualt" outlined v-for="(tag, index) in post.tags" :key="index">
                {{ tag }}
              </v-chip>
            </div>
          </v-card>
        </v-col>
        <v-col cols="12" sm="4" lg="3">
          <v-card class="pa-2 mb-5" elevation="2">
            <p>prev post</p>
            <h2 v-if="post.prev" @click="fetchPostDetail(post.prev.id)" class="my-hover">{{ post.prev.title }}</h2>
          </v-card>
          <v-card class="pa-2 mb-5" elevation="2">
            <p>next post</p>
            <h2 v-if="post.next" @click="fetchPostDetail(post.next.id)" class="my-hover">{{ post.next.title }}</h2>
          </v-card>
          <v-card class="pa-2" elevation="2">
            <h2>Tag cloud</h2>
            <v-chip class="ma-2" color="primary" outlined>
              <v-avatar left class="blue lighten-5">
                1
              </v-avatar>
              python
            </v-chip>
            <v-chip class="ma-2" color="primary" outlined>
              <v-avatar left class="blue lighten-5">
                1
              </v-avatar>
              python
            </v-chip>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",

  data: () => ({
    post: {},
  }),

  created() {
    console.log("created()...");
    const postId = 2;
    this.fetchPostDetail(postId);
  },

  methods: {
    fetchPostDetail(postId) {
      console.log("fetchPostDetail()...");
      axios.get(`/api/post/${postId}/`)
      .then(res => {
        console.log("POST DETAIL GET RES", res);
        this.post = res.data;
      })
      .catch(err=> {
        console.log("POST DETAIL GET ERR.RESPONSE", err.response);
        alert(err.response.status + ' ' + err.response.statusText);
      })
    }
  }
};
</script>

<style scoped>
.my-hover:hover {
  cursor: pointer;
  text-decoration: underline; 
  text-underline-position:under;
  text-decoration-thickness: 1px;
}
</style>
