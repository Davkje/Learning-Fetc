<script setup lang="ts"></script>

<template>
  <main>
    <h1>Home</h1>
    <section>
      <p>
        This is just a landingpage! You'll find the fetched Posts and Todos on their respective
        pages!
      </p>
    </section>
  </main>
</template>

<style lang="scss" scoped>
main {
  background-color: rgb(148, 187, 234);
  margin: 1rem;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-content: center;
  border-radius: 1rem;
  box-shadow: 0px 12px 30px rgba(29, 29, 30, 0.224);
  height: 30vh;
  section {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    p {
      font-size: 1.2rem;
    }
  }
}
</style>
