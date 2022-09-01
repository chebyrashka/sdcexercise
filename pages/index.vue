<template>
    <div class="py-6 px-5">
        <div class="container">
            <Header class="mb-5"
                :header="title"
                :subheader="description">
            </Header>         

            <div class="columns is-tablet">
                <div class="column">
                    <CardPokemon name="Charmander"></CardPokemon>
                </div>

                <div class="column">
                    <CardPokemon name="Bulbasaur"></CardPokemon>
                </div>

                <div class="column">
                    <CardPokemon name="Squirtle"></CardPokemon>
                </div>
            </div>

        </div>
  </div>
</template>

<script>
export default {
    data() {
      return {
        title: 'Pokemon Cards',
        description: 'Gotta catch ‘em all'
      }
    },
    head() {
      return {
        title: this.title,
        meta: [
          {
            hid: 'description',
            name: 'description',
            content: this.description
          }
        ]
      }
    }
}
</script>

