<template>
  <div>
    <Header />
    <h1>{{ details.title }}</h1>
    <h4>{{ details.date }}</h4>
    <component :is="singlePostComponent" />
    <Footer />
  </div>
</template>
<script>
export default {
  async asyncData({ params }) {
    try {
      const post = await import(`~/markdown/${params.slug}.md`)
      return {
        details: post.attributes,
        singlePostComponent: post.vue.component,
      }
    } catch (err) {
      // eslint-disable-next-line
      console.debug(err)
      return false
    }
  },
}
</script>
