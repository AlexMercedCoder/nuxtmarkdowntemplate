/* eslint-disable */

<template>
  <div>
    <Header />
    <h1>My blog posts</h1>
    <ul>
      <li v-for="post in posts" :key="post.attributes.title">
        <nuxt-link :to="post.slug">{{ post.attributes.title }}</nuxt-link>
      </li>
    </ul>
    <Footer />
  </div>
</template>
<script>
export default {
  // eslint-disable-next-line
  async asyncData() {
    const resolve = require.context('~/markdown/', true, /\.md$/)
    const imports = resolve.keys().map((key) => {
      // eslint-disable-next-line
      const [, name] = key.match(/\/(.+)\.md$/)
      //   console.log(name)
      return { ...resolve(key), name, slug: `/mark/${name}` }
    })
    console.log(imports)
    return {
      posts: imports,
    }
  },
}
</script>
