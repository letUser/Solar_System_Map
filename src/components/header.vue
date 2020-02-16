<template>
  <div class="header">
    <ul>
      <li>
        <a>About</a>
      </li>
      <li>
        <a>1</a>
      </li>
      <li>
        <a>1</a>
      </li>
      <li>
        <a>Contact</a>
      </li>
      <li>
        <a>1</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  display: flex;
  position: relative;
  width: 80em;
  margin: 0 auto;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0.589);
  border-radius: 0 0 50% 50% / 0 0 100% 100%;
  opacity: 0.3;
}

.header:hover {
  opacity: 1;
}

ul {
  display: flex;
  justify-content: space-around;
  position: relative;
  width: 40em;
  padding-inline-start: 0;
  margin-block-start: 0;
  margin-block-end: 0;
}

li {
  display: inline-block;
  list-style-type: none;
  padding: 1em 0 1em 0;
}

li a {
  color: rgba(216, 216, 216, 0.904);
  font-size: 1rem;
}
</style>