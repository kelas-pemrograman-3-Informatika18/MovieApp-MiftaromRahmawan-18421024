<template>
  <q-page padding>
    <div class="row q-mb-md col-gutter-md">
      <div class="col-md-12 col-xs-12 col-lg-12">
        <div class="row">
          <div class="col-auto">
            <div class="left blue"></div>
          </div>
          <div class="col">
            <q-banner inline-actions class="text-blue-grey-14">
              <div class="text-h6">Form Edit</div>
              <div>Edit Data DVD film</div>
            </q-banner>
          </div>
        </div>
      </div>
    </div>
    <q-card flat>
      <q-card-section class="row">
        <q-form
        @submit="onSubmit"
          class="q-col-gutter-md q-col-lg-6 col-md-6 col-xs-12"
        >
          <q-input
            filled
            v-model="form.judulFilm"
            label="judul Film *"
            :rules="[ val => val && val.length > 0 || 'mohon isi judul film']"
          />
          <q-input
            filled
            v-model="form.harga"
            label="Harga DVD Film *"
            :rules="[ val => val > 0 || 'mohon isi harga dvd film']"
          />
          <q-input
            filled
            v-model="form.tahun"
            label="tahun Film *"
            :rules="[ val => val && val.length > 0 || 'mohon isi tahun']"
          />
          <q-select
          filled
          v-model="form.genre"
          :options="optionGenre"
          label="genre Film *"
          />
          <div class="flex">
            Pilih rating
            <q-rating
            v-model="form.rating"
            :max="5"
            class="q-ml-md"
            size="32px"
            color="red"
            icon="star_border"
            icon-selected="star"/>
          </div>
          <q-input
          filled
          v-model="form.deskripsi"
          type="textarea"
          label="Deskripsi Film"
          />
          <q-file accept=".jpg, image/*" color="teal" filled v-model="image" label="Upload Gambar">
            <template v-slot:prepend>
              <q-icon name="cloud_upload"/>
            </template>
          </q-file>

          <div>
            <q-btn label="Submit" type="submit" color="primary"/>
            <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
          </div>
        </q-form>
      </q-card-section>
    </q-card>
  </q-page>
</template>
<script>
export default {
  data () {
    return {
      form: {
        judulFilm: null,
        harga: 0,
        tahun: null,
        genre: null,
        rating: 0,
        deskripsi: null
      },
      optionGenre: [
        'Action',
        'Adventure',
        'Comedy',
        'Drama',
        'Fantasy',
        'Tokusatsu'
      ],
      image: null
    }
  },
  created () {
    this.getData()
  },

  methods: {
    getData () {
      this.$axios.get(`movie/getbyid/${this.$route.params.id}`)
        .then(res => {
          if (res.data.sukses) {
            this.form = res.data.data
          } else {
            this.$router.push({ name: 'dataDVD' })
          }
        })
    },
    onSubmit () {
      const formData = new FormData()
      formData.append('image', this.image)
      formData.append('data', JSON.stringify(this.form))
      this.$axios.put(`movie/edit/${this.$route.params.id}`, formData)
        .then(res => {
          if (res.data.sukses) {
            this.$showNotif(res.data.pesan, 'positive')
            this.$router.push({ name: 'dataDVD' })
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
        })
    },

    onReset () {}
  }
}
</script>
<style scoped>
.left {
  width: 5px;
  height: 100%;
  background-color: rgb(229, 245, 0);
}
</style>
