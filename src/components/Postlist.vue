<template>
  <div class="PostList">
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif" />
    </div>
    
    <div class="posts" v-else>
      <ul>
        <li>
          <div class="toobar"></div>
        </li>
        <li class="aa" v-for="post in posts">
          <img :src="post.author.avatar_url"/>
          <span class="bb">
            <span class="reply_count">{{post.reply_count}}</span>
            /{{post.visit_count}}
          </span>

          <span
            :class="[{put_good:(post.good  == true),put_top:(post.top  == true),
        'topiclist-tab':(post.good  != true && post.top  != true)}]"
          >
            <span>
              <span>{{post | tabFormatter}}</span>
            </span>
          </span>

          <router-link
            :to="{
            name:'post_content',
            params:{
              id:post.id,
              name:post.author.loginname
            }
          }"
          >
            <span>{{post.title}}</span>
          </router-link>

          <span class="last_reply">{{post.last_reply_at | formatDate}}</span>
        </li>
        <li>
          <pagination @handleList="renderList"></pagination>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import pagination from "./Pagination";
export default {
  name: "PostList",
  data() {
    return {
      isLoading: false,
      posts: [],
      postpage: 1,
    };
  },
  components: {
    pagination,
  },
  methods: {
    getData() {
      this.$http
        .get("http://rap2api.taobao.org/app/mock/271351/api/v1/topics", {
          params: {
            page: this.postpage,
            limit: 20,
          },
        })
        .then((res) => {
          this.isLoading = false;
          this.posts = res.data.data;
        })
        .catch(function (err) {
          console.log(err);
        });
    },
    renderList(value) {
      this.postpage = value;
      this.getData();
    },
  },
  beforeMount() {
    this.isLoading = true;
    this.getData();
  },
};
</script>

<style scoped>
.PostList {
  background-color: #e1e1e1;
}
.posts {
  padding: 10px;
}
@media (max-width: 678px){
  .posts{
    padding: 0;
  }
}

.PostList img {
  height: 30px;
  width: 30px;
  vertical-align: middle;
}

ul {
  list-style: none;
  width: 100%;
  max-width: 1400px;
  margin: 0 auto;
}
@media (max-width: 678px){
  ul{
    padding: 0;
  }
}
ul li:not(:first-child) {
  padding: 9px;
  font-size: 15px;
  font-family: "Helvetica Neue", "Luxi Sans", "DejaVu Sans", Tahoma,
    "Hiragino Sans GB", STHeiti, sans-serif !important;
  font-weight: 400;
  background-color: white;
  color: #333;
  border-top: 1px solid #f0f0f0;
}
@media (max-width: 678px){
  ul li:not(:first-child){
    position: relative;
    padding: 10px 0 10px 10px;
    font-size: 14px;
    overflow: hidden;
    height: 40px;
  }
}
@media (max-width: 678px){
  .aa{
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
  }
}
@media (max-width: 678px){
  .bb{
    position: absolute;
    bottom: 0;
    left: 85px;
    text-align: left;
    font-size: 12px;
  }
}
li:not(:first-child):hover {
  background: #f5f5f5;
}

li:last-child:hover {
  background: white;
}

li span {
  line-height: 30px;
}

.allcount {
  width: 70px;
  display: inline-block;
  text-align: center;
  font-size: 12px;
}

.reply_count {
  color: #9e78c0;
  font-size: 12px;
}

.put_good,
.put_top {
  background: #80bd01;
  padding: 2px 4px;
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  -o-border-radius: 3px;
  color: #fff;
  font-size: 12px;
  margin-right: 10px;
}
@media (max-width: 678px){
  .put_top{
    margin: 0;
  }
}

.topiclist-tab {
  background-color: #e5e5e5;
  color: #999;
  padding: 2px 4px;
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  -o-border-radius: 3px;
  font-size: 12px;
  margin-right: 10px;
}

.last_reply {
  text-align: right;
  min-width: 50px;
  display: inline-block;
  white-space: nowrap;
  float: right;
  color: #778087;
  font-size: 12px;
}

@media (max-width: 678px){
  .last_reply{
    position: absolute;
    bottom: 0;
    right: 10px;
    font-size: .8em;
  }
}

.toobar {
  height: 40px;
  background-color: #f5f5f5;
}

.toobar span {
  font-size: 14px;
  color: #80bd01;
  line-height: 40px;
  margin: 0 10px;
  cursor: pointer;
}

.toobar span:hover {
  color: #9e78c0;
}

a {
  text-decoration: none;
  color: black;
}

a:hover {
  text-decoration: underline;
}

.loading {
  text-align: center;
  padding-top: 300px;
}
</style>