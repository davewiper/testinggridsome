<template>
  <Layout>
    <div class="has-text-centered">
      <h1 class="title is-1">
        {{ $page.post.title }}
      </h1>
      <PostMeta
        class="subtitle is-size-6"
        :post="$page.post"
      />
    </div>

    <div class="post content section container">
      <figure
        v-if="$page.post.coverImage"
        class="image is-16by9"
      >
        <g-image
          alt="Cover image"
          :src="$page.post.coverImage"
        />
      </figure>

      <p v-html="$page.post.content" />

      <footer>
        <PostTags :post="$page.post" />
      </footer>
    </div>

    <div class="post-comments">
      <!-- Add comment widgets here -->
    </div>
  </Layout>
</template>

<script>
import PostMeta from '~/components/PostMeta';
import PostTags from '~/components/PostTags';

export default {
  components: {
    PostMeta,
    PostTags,
  },
  metaInfo() {
    return {
      title: this.$page.post.title,
      meta: [
        {
          name: 'description',
          content: this.$page.post.description,
        },
      ],
    };
  },
};
</script>

<page-query>
query Post($path: String!) {
  post: post(path: $path) {
    title
    path
    date(format: "D. MMMM YYYY")
    timeToRead
    tags {
      id
      title
      path
    }
    description
    content
    cover_image(width: 860, blur: 10)
  }
}
</page-query>
