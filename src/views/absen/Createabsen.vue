<template>
<div class="card shadow mt-3">
  <div class="card-body">
    <h5 class="card-title">Add Absen</h5>
     <form class="row g-3" @submit.prevent="store">
  <div class="col-md-6">
    <label for="inputEmail4" class="form-label">Waktu Absen</label>
    <input type="time" class="form-control" id="inputEmail4" 
    v-model="presents.waktu_absen" />
      <div class="alert alert-danger" v-if="validation.waktu_absen">
        {{ validation.waktu_absen[0] }}
      </div>
  </div>
  <div class="col-md-6">
    <label for="inputEmail4" class="form-label">Nama Mahasiswa</label>
    <input type="text" class="form-control" id="inputEmail4" 
    v-model="presents.mahasiswa_id" />
      <div class="alert alert-danger" v-if="validation.mahasiswa_id">
        {{ validation.mahasiswa_id[0] }}
      </div>
  </div>
  <div class="col-md-6">
    <label for="inputPassword4" class="form-label">Nama Matakuliah</label>
    <input type="text" class="form-control" id="inputPassword4"
    v-model="presents.matakuliah_id"/>
    <div class="alert alert-danger" v-if="validation.matakuliah_id">
        {{ validation.matakuliah_id[0] }}
      </div>
  </div>
  <div class="col-12">
    <label for="inputAddress" class="form-label">Keterangan</label>
    <input type="text" class="form-control" id="inputAddress" 
    v-model="presents.keterangan" />
    <div class="alert alert-danger" v-if="validation.keterangan">
        {{ validation.keterangan[0] }}
      </div>
  </div>
  
  <div class="col-12">
    <button type="submit" class="btn btn-primary">Add</button>
  </div>
</form>
  </div>
</div>
 
</template>
<script>
import { ref } from 'vue';
import { reactive } from 'vue';
import { useRouter } from 'vue-router'
import axios from 'axios'
export default {
  setup() {

    const presents = reactive({
      waktu_absen: '',
      mahasiswa_id: '',
      matakuliah_id: '',
      keterangan: ''
      
    })

    const validation = ref([])

    const router = useRouter()

    function store(){
      let waktu_absen = presents.waktu_absen
      let mahasiswa_id = presents.mahasiswa_id
      let matakuliah_id = presents.matakuliah_id
      let keterangan = presents.keterangan

      axios.post('http://127.0.0.1:8000/api/presents', {
        waktu_absen: waktu_absen,
        mahasiswa_id: mahasiswa_id,
        matakuliah_id: matakuliah_id,
        keterangan: keterangan
        
      }).then(() => {
        router.push({
          name:'Absen'
        })
      }).catch(error => {
        console.log(error)
      })
    }
    return {
      presents,
      validation,
      router, 
      store
    }
  },
}
</script>
