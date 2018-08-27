<template>
    <div class="about">
        <h1>Hello {{their_name}}. This is an about page</h1>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Explicabo commodi, natus sunt quasi facere reprehenderit rerum quae? Eaque earum est eius accusamus enim, doloribus aspernatur odio omnis eveniet a assumenda!</p>
    </div>
</template>

<script>
export default {
  name: "About",
  data() {
    return {
      their_name: this.$route.params.name
    };
  }
};
</script>
