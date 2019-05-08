<template>
  <div>
  </div>
</template>

<script>
export default {
    name: "Graph",
    mounted() {
        this.$root.$on('click', (e) => {
            console.log(e)
        })
    }
}
</script>

