<template>
  <div>
    <h1>Home</h1>
    <p>Content for the blog is in the ./content directory</p>
    <h2>Latest 3 Posts</h2>
    <ul>
      <li v-for="post in posts" :key="post.slug">
        <h3>{{ post.title }}</h3>
        <p>{{ $dateFns.format(post.date, 'do MMMM yyyy') }}</p>
        <small><n-link :to="`/blog/${post.slug}`">Read More</n-link></small>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const posts = await $content('blog').sortBy('date', 'desc').limit(3).fetch()
    return { posts }
  },
}
</script>
