<script>
import { ref } from 'vue'

export default {
  setup() {
    const nama = ref('')
    const hitungan = ref(0)
    const urlStatus = ref('https://youtu.be/Y7jQovKCJSE?si=3fsHDN4cDpVQWRce')
    
    // status tombol
    const aktif = ref(false)
    const warnaTeks = ref('blue')
    const ukuranFont = ref(18)
    const tebal = ref(true)
    
    // Menambahkan variabel untuk conditional rendering
    const tampilkanHitungan = ref(true)
    const jenisUser = ref('tamu')
    const adaError = ref(true)
    const pesan = ref('')
    
    function toggleAktif() {
      aktif.value = !aktif.value
    }
    
    function toggleTampilkanHitungan() {
      tampilkanHitungan.value = !tampilkanHitungan.value
    }
    
    function ubahJenisUser() {
      jenisUser.value = jenisUser.value === 'tamu' ? 'admin' : 'tamu'
    }
    
    setTimeout(() => {
      aktif.value = true
      warnaTeks.value = 'green'
      adaError.value = false
    }, 2000)
    
    function tambahHitungan() {
      hitungan.value++
      if (hitungan.value > 5) {
        pesan.value = 'Anda telah mengklik lebih dari 5 kali!'
      }
    }
    
    return {
      nama,
      hitungan,
      tambahHitungan,
      warnaTeks,
      ukuranFont,
      tebal,
      urlStatus,
      toggleAktif,
      tampilkanHitungan,
      toggleTampilkanHitungan,
      jenisUser,
      ubahJenisUser,
      adaError,
      pesan
    }
  }
}
</script>

<template>
  <div>
    <!-- Conditional rendering menggunakan v-if -->
    <div v-if="adaError" style="color: red; background-color: #ffeeee; padding: 10px; border: 1px solid red; margin-bottom: 10px;">
      Terjadi kesalahan. Silakan tunggu sebentar...
    </div>
    
    <div>
      <label>Nama:</label>
      <input v-model="nama" type="text" placeholder="Masukkan nama" />
      <p>Nama yang dimasukkan: {{ nama }}</p>
    </div>
    

    <div>
      <button @click="toggleTampilkanHitungan">{{ tampilkanHitungan ? 'Sembunyikan' : 'Tampilkan' }} Hitungan</button>
      <div v-if="tampilkanHitungan">
        <button @click="tambahHitungan">Klik saya</button>
        <p>Jumlah klik: {{ hitungan }}</p>
        
 
        <p v-if="pesan" style="color: orange;">{{ pesan }}</p>
      </div>
      <p v-else>Hitungan disembunyikan</p>
    </div>
    
    <div>
      <a :href="urlStatus" target="_blank">Kunjungi Website Ini</a>
    </div>
    
    <button :disabled="!aktif">
      {{ aktif ? 'Tombol Aktif' : 'Tombol Tidak Aktif' }}
    </button>
    

    <div style="margin-top: 20px;">
      <button @click="ubahJenisUser">Ubah Jenis User</button>
      <div v-if="jenisUser === 'admin'" style="background-color: #eeffee; padding: 10px; margin-top: 10px;">
        <h3>Panel Admin</h3>
        <p>Selamat datang, Admin! Anda memiliki akses penuh.</p>
      </div>
      <div v-else-if="jenisUser === 'tamu' && nama" style="background-color: #eeeeff; padding: 10px; margin-top: 10px;">
        <h3>Panel Tamu</h3>
        <p>Selamat datang, {{ nama }}! Anda memiliki akses terbatas.</p>
      </div>
      <div v-else style="background-color: #ddd; padding: 10px; margin-top: 10px;">
        <h3>Panel Pengunjung</h3>
        <p>Silakan masukkan nama Anda untuk melanjutkan.</p>
      </div>
    </div>
    
    <p :style="{color: warnaTeks, fontSize: ukuranFont + 'px', fontWeight: tebal ? 'bold' : 'normal'}">
      TEKS DENGAN GAYA DINAMIS
    </p>
  </div>
</template>