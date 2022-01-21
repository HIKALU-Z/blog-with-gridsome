<template>
  <Layout>
    <!-- Page Header-->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(http://120.24.73.121:1337${general &&
          general.cover &&
          general.cover.url})`,
      }"
    >
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <!-- post form strapi  -->
          <div
            class="post-preview"
            v-for="post in onlinePosts"
            :key="post.node.id"
          >
            <g-link :to="`post/${post.node.id}`">
              <h2 class="post-title">
                {{ post.node.title }}
              </h2>
              <h3 class="post-subtitle">
                {{ post.node.title }}
              </h3>
            </g-link>
            <p class="post-meta">
              Posted by
              <a href="#!">{{ post.node.create_by.username }}</a>
              on {{ transformDate(post.node.created_at) }}
            </p>
            <p>
              <span v-for="tag in post.node.tags" :key="tag.id">
                <a href="">{{ tag.name }}</a
                >&nbsp;&nbsp;
              </span>
            </p>
            <!-- Divider-->
            <hr class="my-4" />
          </div>
          <!-- post form md -->
          <div
            class="post-preview"
            v-for="post in mdPosts"
            :key="post.node.id"
            v-if="false"
          >
            <a href="post.html">
              <h2 class="post-title">
                {{ post.node.title }}
              </h2>
              <h3 class="post-subtitle">
                {{ post.node.title }}
              </h3>
            </a>
            <p class="post-meta">
              Posted by
              <a href="#!">HIKALU</a>
              on September 24, 2021
            </p>

            <!-- Divider-->
            <hr class="my-4" />
          </div>

          <!-- Pager-->
          <div class="d-flex justify-content-end mb-4" v-if="false">
            <a class="btn btn-primary text-uppercase" href="#!">
              Older Posts →
            </a>
          </div>
          <Pager :info="$page.onlinePosts.pageInfo" class="my-pager"></Pager>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query($page:Int){
 allStrapiGeneral{
    edges{
      node{
        title
        subtitle
        cover{
          url
        }
      }
    }
  }
  mdPosts:allMdPost{
    edges{
      node{
        id
        title
        path
        content
      }
    }
  }
  onlinePosts:allStrapiPost(perPage:2,page:$page) @paginate{
    pageInfo{
      totalPages
      currentPage
    }
    edges{
      node{
        id
        title
        cover{
          url
        }
        tags{
          id
          name
        }
        content
        created_at
        create_by {
          username
        }
      }
    }
  }
}
</page-query>

<script>
import * as dayjs from "dayjs";
import { Pager } from "gridsome";

export default {
  components: {
    Pager,
  },
  name: "IndexPage",
  metaInfo: {
    title: "Hello, world!",
  },
  computed: {
    mdPosts() {
      return this.$page.mdPosts.edges;
    },
    onlinePosts() {
      return this.$page.onlinePosts.edges;
    },
    general() {
      return this.$page.allStrapiGeneral.edges[0].node;
    },
  },
  methods: {
    transformDate(date) {
      return dayjs(date).format("YYYY-MM-DD");
    },
  },
  mounted() {
    console.log("md-posts", this.mdPosts);
    console.log("online-posts", this.onlinePosts);
    console.log("general", this.general);
  },
};
</script>

<style>
.my-pager {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
  width: 100%;
}
.my-pager a {
  font-size: 24px;
}
.my-pager a + a {
  margin-left: 20px;
}
.my-pager a:hover {
  color: teal;
}
</style>
