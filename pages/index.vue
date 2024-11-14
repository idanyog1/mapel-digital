<template>
  <div class="container">
    <div class="text-center mb-5">
      <h1>MATA PELAJARAN</h1>
    </div>
    <div v-if="mapels.length === 0" class="text-center">
      <p>Loading...</p>
    </div>
    <div class="row" v-else>
      <div v-for="(mapel, i) in mapels" :key="i" class="col-4 my-5">
        <nuxt-link :to="`/mapel/${mapel.id}`">
          <div class="card" style="width: 18rem;">
            <div class="card-body m-5 px-5">
              <h3 class="card-title">{{ mapel.name }}</h3>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const mapels = ref([])

const getHari = async () => {
  const { data, error } = await supabase.from('hari').select('*')
  if (data) {
    mapels.value = data
  } else if (error) {
    console.error("Error fetching data:", error)
  }
}

onMounted(() => {
  getHari()
})
</script>

<style scoped>
.row {
  margin-top: 100px;
  display: flex;
  justify-content: center;
}

.card {
  background-color: rgb(13, 144, 236);
  color: white;
  display: block;
}

.card-body {
  padding: 20px;
  text-align: center;
}

.text-center p {
  font-size: 20px;
  color: #888;
}
</style>
