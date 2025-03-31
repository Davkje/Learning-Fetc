<script setup lang="ts">
fetch('http://localhost:3000/posts')
  .then((response) => {
    // console.log(response)
    return response.json()
  })
  .then((data) => {
    const postElement = document.getElementById('postContainer')

    postElement.innerHTML = data
      .map(
        (post) => `
      <div class="post">
        <h3>${post.title}</h3>
        <span class="content">${post.content}</span>
        <span class="author">${post.author}</span>  
      </div> 
    `,
      )
      .join('')
  })
  .catch((error) => {
    console.log(error)
  })
</script>

<template>
  <main>
    <h1>Posts</h1>
    <form id="topSection">
      <input type="text" class="form-control" id="search" placeholder="Search" name="search" />
      <select class="form-select" id="sort" name="sort" onchange="fetchPosts(event)">
        <option>Sort</option>
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
      </select>
    </form>
    <div id="postContainer" class="post-container"></div>
  </main>
</template>

<style lang="scss" scoped>
main {
  background-color: rgb(233, 172, 219);
  margin: 1rem;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  border-radius: 1rem;
  box-shadow: 0px 12px 30px rgba(29, 29, 30, 0.224);
}
</style>
