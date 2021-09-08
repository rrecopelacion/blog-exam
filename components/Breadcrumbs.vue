<template>
  <div class="breadcrumbs">
    <div class="l-container">
      <ul class="flex">
        <li class="breadcrumbs-item">
          <nuxt-link to="/">HOME</nuxt-link>
        </li>
        <li class="breadcrumbs-item">{{title}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Breadcrumbs',
  props: ['title'],
}
</script>

<style scoped lang="scss" src="./Breadcrumbs.scss">
