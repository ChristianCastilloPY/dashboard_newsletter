<template>
  <div class="container" style="margin:0px;padding:0px">
    <div class="d-flex flex-nowrap" style>
      <div class="bg-dark " style="height:100vh;width:200px">
        <div class="mt-5 ml-3">
          <a
            :href="'/dashboard/newsletters' + '/' + 'all'"
            to="/todo"
            style="text-decoration: none; color:rgba(180,200,211,0.9)"
            >All</a
          >
          <div v-for="(button, index) in buttons" :key="index" class="mt-2">
            <!-- <a :href=" '/tags' + '?' +  button.name "> -->
            <a
              :href="'/dashboard/newsletters' + '/' + button.slug"
              style="text-decoration: none; color:rgba(180,200,211,0.9)"
              >{{ button.name }}</a
            >
          </div>
        </div>
      </div>
      <div class=" w-100" style="margin:0px;padding:0px">
        <a href="/all">
          <button
            type="button"
            class="m-1 btn btn-light bg-light border-0"
            style="color:gray"
          >
            HOME
          </button>
        </a>
        <div class="d-flex justify-content-start ml-5 mt-2 bg-gray">
          <h3>Logo</h3>
        </div>
        <h5 class="ml-3 gray">Presiona algun boton de la izquierda</h5>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      buttons: []
    }
  },
  created() {
    this.getTags()
  },
  methods: {
    getTags() {
      const url2 = 'https://newsletters.academlo.com/api/v1/tags'
      axios
        .get(url2)
        .then((response) => {
          this.buttons = response.data
        })
        .catch((error) => {
          console.log(error.response)
        })
    }
  }
}
</script>
