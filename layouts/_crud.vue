<template>
  <div class="container">
    <div class="d-flex flex-nowrap" style="height:100vh">
      <div
        class="bg-dark"
        style="height:100vh;width:200px;margin-left:-130px                            "
      >
        <div class="mt-5 ml-5 mr-5">
          <a
            :href="'/dashboard/newsletters' + '/' + 'all'"
            style="text-decoration: none; color:rgba(180,200,211,0.9)"
            >All</a
          >
          <div v-for="(button, index) in buttons" :key="index" class="mt-2">
            <!-- <a :href=" '/tags' + '?' +  button.name "> -->
            <a
              :href="'/dashboard/newsletters' + '/' + button.slug"
              style="text-decoration: none; color:rgba(180,200,211,0.9)"
            >
              {{ button.name }}
            </a>
          </div>
        </div>
      </div>

      <div class="w-100" style="margin:0px;padding:0px">
        <a href="/all">
          <button
            type="button"
            class="m-1 btn btn-light bg-light border-0"
            style="color:gray"
          >
            HOME
          </button>
        </a>
        <div class="    d-flex justify-content-between">
          <h3
            class="w-90 mt-3 mb-3 navbar navbar-expand-lg navbar-light bg-light"
          >
            Newsletter = {{ slug.post }}
          </h3>
        </div>

        <div v-if="AddformActualizar == true">
          <section class="form">
            <form action="" class="text-center">
              <input
                v-model="title"
                @keyup.enter="crearPaciente"
                type="text"
                name="title"
                class="form-control"
                placeholder="title"
              />
              <input
                v-model="description"
                @keyup.enter="crearPaciente"
                type="text"
                name="description"
                class="form-control"
                placeholder="description"
              />
              <input
                v-model="target"
                @keyup.enter="crearPaciente"
                type="text"
                name="target"
                class="form-control"
                placeholder="target"
              />
              <input
                v-model="subscribed"
                @keyup.enter="crearPaciente"
                type="text"
                name="subscribed"
                class="form-control"
                placeholder="subscribed"
              />
              <input
                v-model="image"
                @keyup.enter="crearPaciente"
                name="image"
                type="text"
                class="form-control"
                placeholder="image"
              />
              <!-- Botón para añadir -->
              <input
                @click="crearPaciente"
                type="button"
                value="Añadir"
                class="btn btn-success"
              />
            </form>
          </section>
        </div>
        <div class="ml-3 mt-2">
          <button
            class="btn btn-secondary my-2 ml-2 my-sm-0"
            @click="Agregar()"
            type="submit"
          >
            Agregar
          </button>
        </div>

        <div v-if="this.$route.params.post === 'all'">
          <section class="data">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">Title</th>
                  <th scope="col">Description</th>
                  <th scope="col">Target</th>
                  <th scope="col">Subscribed</th>
                  <th scope="col">Image</th>
                  <th></th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(card, index) in cards" :key="index">
                  <!-- <td>{{ card.title }}</td> -->
                  <td>
                    <span
                      v-if="formActualizar && idActualizar == index"
                      class=""
                    >
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="nombreActualizar"
                        type="text"
                        class="form-control "
                      />
                    </span>
                    <span v-else>
                      <!-- Dato nombre -->
                      {{ card.title }}
                    </span>
                  </td>
                  <td>
                    <span
                      v-if="formActualizar && idActualizar == index"
                      class=""
                    >
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="descriptionActualizar"
                        type="text"
                        class="form-control "
                      />
                    </span>
                    <span v-else>
                      <!-- Dato nombre -->
                      {{ card.description }}
                    </span>
                  </td>
                  <td>
                    <span v-if="formActualizar && idActualizar == index">
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="targetActualizar"
                        type="text"
                        class="form-control"
                      />
                    </span>
                    <span v-else>
                      <!-- Dato edad -->
                      {{ card.target }}
                    </span>
                  </td>
                  <td>
                    <span v-if="formActualizar && idActualizar == 0">
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="subscribedActualizar"
                        type="text"
                        class="form-control"
                      />
                    </span>
                    <span v-else>
                      <!-- Dato edad -->
                      {{ card.subscribed }}
                    </span>
                  </td>
                  <td>
                    <span v-if="formActualizar && idActualizar == index">
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="imageActualizar"
                        type="text"
                        class="form-control"
                      />
                    </span>
                    <span v-else>
                      <!-- Dato edad -->
                      <img :src="card.image" style="height:50%" />
                    </span>
                  </td>
                  <td>
                    <!-- Botón para guardar la información actualizada -->
                    <span v-if="formActualizar && idActualizar == index">
                      <button
                        @click="guardarActualizacion(index)"
                        class="btn btn-success"
                      >
                        Guardar
                      </button>
                    </span>
                    <span v-else>
                      <!-- Botón para mostrar el formulario de actualizar -->
                      <button
                        @click="verFormActualizar(index)"
                        class="btn btn-warning mb-2"
                      >
                        Actualizar
                      </button>
                      <!-- Botón para borrar -->
                      <button
                        @click="borrarPaciente(index)"
                        class="btn btn-danger"
                      >
                        Borrar
                      </button>
                    </span>
                  </td>
                </tr>
              </tbody>
            </table>
          </section>
        </div>

        <div v-else>
          <section class="data">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">Title</th>
                  <th scope="col">Description</th>
                  <th scope="col">Target</th>
                  <th scope="col">Subscribed</th>
                  <th scope="col">Image</th>
                  <th></th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(card, index2) in cardstag.newsletters"
                  :key="index2"
                >
                  <td>
                    <span
                      v-if="formActualizardos && idActualizardos == index2"
                      class=""
                    >
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="nombreActualizardos"
                        type="text"
                        class="form-control "
                      />
                    </span>
                    <span v-else>
                      <!-- Dato nombre -->
                      {{ card.title }}
                    </span>
                  </td>
                  <td>
                    <span
                      v-if="formActualizardos && idActualizardos == index2"
                      class=""
                    >
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="descriptionActualizard"
                        type="text"
                        class="form-control "
                      />
                    </span>
                    <span v-else>
                      <!-- Dato nombre -->
                      {{ card.description }}
                    </span>
                  </td>
                  <td>
                    <span v-if="formActualizardos && idActualizardos == index2">
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="targetActualizardos"
                        type="text"
                        class="form-control"
                      />
                    </span>
                    <span v-else>
                      <!-- Dato edad -->
                      {{ card.target }}
                    </span>
                  </td>
                  <td>
                    <span v-if="formActualizardos && idActualizardos == index2">
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="subscribedActualizardos"
                        type="text"
                        class="form-control"
                      />
                    </span>
                    <span v-else>
                      <!-- Dato edad -->
                      {{ card.subscribed }}
                    </span>
                  </td>
                  <td>
                    <span v-if="formActualizardos && idActualizardos == index2">
                      <!-- Formulario para actualizar -->
                      <input
                        v-model="imageActualizardos"
                        type="text"
                        class="form-control"
                      />
                    </span>
                    <span v-else>
                      <!-- Dato edad -->
                      <img :src="card.image" style="height:50%" />
                    </span>
                  </td>
                  <td>
                    <!-- Botón para guardar la información actualizada -->
                    <span v-if="formActualizardos && idActualizardos == index2">
                      <button
                        @click="guardarActualizaciondos(index2)"
                        class="btn btn-success"
                      >
                        Guardar
                      </button>
                    </span>
                    <span v-else>
                      <!-- Botón para mostrar el formulario de actualizar -->
                      <button
                        @click="verFormActualizardos(index2)"
                        class="btn btn-warning mb-2"
                      >
                        Actualizar
                      </button>
                      <!-- Botón para borrar -->
                      <button
                        @click="borrarPacientedos(index2)"
                        class="btn btn-danger"
                      >
                        Borrar
                      </button>
                    </span>
                  </td>
                </tr>
              </tbody>
            </table>
          </section>
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
      isToggled: true,
      // Input nombre
      nombre: '',
      // Input edad
      edad: '',
      // Ver o no ver el formulario de actualizar
      formActualizar: false,
      formActualizardos: false,
      // La posición de tu lista donde te gustaría actualizar
      idActualizar: -1,
      idActualizardos: -1,
      // Input nombre dentro del formulario de actualizar
      nombreActualizar: '',
      // Input edad dentro del formulario de actualizar
      descriptionActualizar: '',
      edadActualizar: '',
      targetActualizar: '',
      subscribedActualizar: '',
      imageActualizar: '',
      AddformActualizar: false,
      descriptionActualizard: '',
      nombreActualizardos: '',
      targetActualizardos: '',
      subscribedActualizardos: '',
      imageActualizardos: '',
      // ruta: this.window.location.href,
      cards: [],
      cardstag: [],
      buttons: [],
      slug: this.$route.params
    }
  },
  mounted() {
    this.getCards()
    this.getCARDS()
  },
  created() {
    this.getTags()
  },
  methods: {
    crearPaciente() {
      this.AddformActualizar = false
      // Anyadimos a nuestra lista
      const endPointed = 'https://newsletters.academlo.com/api/v1/newsletters'
      this.cards.push({
        id: new Date(),
        title: this.title,
        description: this.description,
        target: this.target,
        subscribed: this.subscribed,
        image: this.image
      })

      console.log(this.cards[this.cards.length - 1])
      axios
        .post(endPointed, this.cards[this.cards.length - 1])
        .then((response) => {
          console.log(response.data)
          alert('Se creo exitosamente el boletin')
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
    },

    Agregar() {
      this.AddformActualizar = true
    },
    verFormActualizar(index) {
      this.idActualizar = index
      // Antes de mostrar el formulario de actualizar, rellenamos sus campos
      this.nombreActualizar = this.cards[index].title
      this.descriptionActualizar = this.cards[index].description
      this.targetActualizar = this.cards[index].target
      this.subscribedActualizar = this.cards[index].subscribed
      this.imageActualizar = this.cards[index].image
      this.formActualizar = true
    },
    verFormActualizardos(dos) {
      this.idActualizardos = dos
      this.nombreActualizardos = this.cardstag.newsletters[dos].title
      this.descriptionActualizard = this.cardstag.newsletters[dos].description
      this.targetActualizardos = this.cardstag.newsletters[dos].target
      this.subscribedActualizardos = this.cardstag.newsletters[dos].subscribed
      this.imageActualizardos = this.cardstag.newsletters[dos].image
      // Mostramos el formulario
      this.formActualizardos = true
    },
    borrarPaciente(index) {
      // Borramos de la lista
      console.log(index)

      const endPoint =
        'https://newsletters.academlo.com/api/v1/newsletters/' +
        this.cards[index].id
      console.log(endPoint)
      console.log(this.cards[index].id)
      axios
        .delete(endPoint)
        .then((response) => {
          alert('Se elimino exitosamente el boletin')
          console.log('Se elimino correctamente')
        })
        .catch(() => {
          alert('Tuvimos un error')
        })

      this.cards.splice(index, 1)
    },
    borrarPacientedos(index) {
      // Borramos de la lista
      console.log(index)

      const endPoint =
        'https://newsletters.academlo.com/api/v1/newsletters/' +
        this.cardstag.newsletters[index].id
      console.log(endPoint)
      console.log(this.cardstag.newsletters[index].id)
      axios
        .delete(endPoint)
        .then((response) => {
          alert('Se elimino exitosamente el boletin')
          console.log('Se elimino correctamente')
        })
        .catch(() => {
          alert('Tuvimos un error')
        })

      this.cardstag.newsletters.splice(index, 1)
    },
    guardarActualizacion(index) {
      // Ocultamos nuestro formulario de actualizar
      this.formActualizar = false
      // Actualizamos los datos
      this.cards[index].title = this.nombreActualizar
      this.cards[index].description = this.descriptionActualizar
      this.cards[index].target = this.targetActualizar
      this.cards[index].subscribed = this.subscribedActualizar
      this.cards[index].image = this.imageActualizar
    },
    guardarActualizaciondos(dos) {
      this.formActualizardos = false

      this.cardstag.newsletters[dos].title = this.nombreActualizardos
      this.cardstag.newsletters[dos].description = this.descriptionActualizard
      this.cardstag.newsletters[dos].target = this.targetActualizardos
      this.cardstag.newsletters[dos].subscribed = this.subscribedActualizardos
      this.cardstag.newsletters[dos].image = this.imageActualizardos
    },
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
    },
    getCARDS() {
      const URL_N = `https://newsletters.academlo.com/api/v1/newsletters`
      axios.get(URL_N).then((response) => {
        this.cards = response.data
        // console.log(this.cards)
      })
    },
    getCards() {
      this.URL_N = `https://newsletters.academlo.com/api/v1/tags/${this.slug.post}?include=newsletters`
      this.$axios.get(this.URL_N).then((response) => {
        this.cardstag = response.data
        console.log(this.cardstag)
      })
    }
  }
}
</script>
