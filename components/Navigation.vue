<template>
  <div id="browse">
    <div class="nav w-100 bg-light">
      <div class="w-100 mt-4 bg-light" style="color:orange;height:50px">
        <div class="ml-5 d-flex justify-content-between">
          <div>
            <h2 class="font-weight-bold">[ INSIDE ]</h2>
          </div>
          <div class="mr-2">
            <h3>
              <fa :icon="['fas', 'search']" />
              <fa :icon="['fas', 'user']" />
            </h3>
            <a href="/dashboard/newsletters">
              <button
                type="button"
                class="m-1 btn btn-light bg-light border-0"
                style="color:orange"
              >
                Dashboard
              </button>
            </a>
          </div>
        </div>
      </div>
      <br />
      <br />

      <div class="btn-group btn-group-toggle mt-4">
        <a href="all" to="/all">
          <button
            type="button"
            class="m-1 btn btn-light bg-light border-0"
            style="color:gray"
          >
            All
          </button>
        </a>
      </div>

      <div class="btn-group btn-group-toggle list-inline mt-4">
        <div
          v-for="(button, index) in buttons"
          :key="index"
          style="col-md-2"
          class="list-inline-item"
        >
          <!-- <a :href=" '/tags' + '?' +  button.name "> -->
          <a :href="'/tags' + '?' + button.slug">
            <button
              type="button"
              class="m-1 btn btn-light bg-light border-0"
              style="color:gray"
            >
              {{ button.name }}
            </button>
          </a>
        </div>
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
