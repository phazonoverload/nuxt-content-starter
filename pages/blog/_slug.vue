<template>
  <div>
    <h1>{{ post.title }}</h1>
    <small>Posted {{ $dateFns.format(post.date, 'do MMMM yyyy') }}</small>
    <article>
      <nuxt-content :document="post" />
    </article>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const post = await $content('blog', params.slug).fetch()
    return { post }
  },
  head() {
    return {
      title: this.post.title,
    }
  },
}
</script>
