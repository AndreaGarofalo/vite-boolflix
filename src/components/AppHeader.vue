<script>
export default {
  name: "Boolflix Header",
};
</script>

<template>
  <header>
    <div class="container">
      <div class="header-content">
        <h2>Boolflix</h2>
        <div class="searchbar">
          <input type="text" />
          <button class="text-light">Cerca</button>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped lang="scss">
header {
  background-color: black;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 60px;
  .container {
    height: 100%;
    .header-content {
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      h2 {
        color: red;
      }
      button {
        background-color: red;
      }
    }
  }
}
</style>
