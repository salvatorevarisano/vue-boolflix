<template>
  <header>
        <h1>
            <a href="#">
              <img src="https://fontmeme.com/permalink/210512/c072857f28ffed69c9266a55183f4c20.png" alt="boolflix">
            </a>
        </h1>
      <form>
          <input type="text" v-model.trim="keyword" >
          <button type="submit" @click.prevent="$emit('searchKeyword', keyword)"><i class="fas fa-search"></i></button>
      </form>
  </header>
</template>

<script>
export default {
    name: 'Header',

    data() {
        return {
            keyword: '',
        }
    }
}
</script>

<style lang="scss" scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 90px;
        .brand {
            height: 100%;

            svg {
                height: 100%;
                fill: #e50914;
            }
        }
    }
</style>