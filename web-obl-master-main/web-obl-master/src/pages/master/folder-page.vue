<template>
  <div class="background-container">
  <h1>
    <div class="heading1">
      <center>INI ADALAH TABEL DATA YANG TELAH DIINPUT</center>
    </div>
  </h1>
  <div class="table">
  <div class="table-row">
    <div class="table-cell header">Keterangan</div>
    <div class="table-cell header">Dokumen</div>
    <div class="table-cell header">Aksi</div>
  </div>
  <div class="table-row">
    <div class="table-cell">OBL</div>
    <div class="table-cell"><a v-if="document && document.OBL.id">{{ document.OBL.id }}</a></div>
    <div class="table-cell">
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>  
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">AM</div>
    <div class="table-cell"><p v-if="document && document.AM.id">{{ document.AM.id }}</p></div>
    <div class="table-cell">
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">SPPII/BA Visit</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell">
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">P0</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell">
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">P1</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell">
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">Quotation</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell">
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">Surat Penunjukan</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell">
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">Kontrak KD</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell"> 
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">KL/WC</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell"> 
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <div class="table-row">
    <div class="table-cell">Mitra OBL</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell"> 
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
    <div class="table-row">
    <div class="table-cell">Dokumen Pendukung Lainnya</div>
    <div class="table-cell"><a href="file1.pdf" target="_blank">File 1</a></div>
    <div class="table-cell"> 
      <button class="btn-update">Update</button>
      <button class="btn-delete">Delete</button>
    </div>
  </div>
  <!-- Tambahkan lebih banyak baris sesuai kebutuhan -->
</div>


  <div class="back-button-container">
    <router-link to="/dashboard" class="back-button">Kembali</router-link>
  </div>
  </div>
</template>


<script>
import axios from 'axios';
import { onMounted, ref } from 'vue';

export default {
setup(){
    const documents = ref([]);
    const url = "http://localhost:4000/users";
    const showDropDown = ref(false);
    const showSide = ref(true);

    async function getDocument() {
    try {
        const response = await axios.get(url);
        const data = response.data.data;

        const documentsWithDefaults = data.map(document => ({
            ...document,
            OBL: document.OBL || 'Not available',
            AM: document.AM || 'Not available',
        }));

        documents.value = documentsWithDefaults;
    } catch (error) {
        console.error(error);
    }
}

    const toggleSideBar = () => {
        showSide.value = !showSide.value;
    };

    const toggleDrop = () => {
        showDropDown.value = !showDropDown.value;
    };

    onMounted(() => {
        getDocument();
    });

    return {
        documents,
        showDropDown,
        showSide,
        toggleSideBar,
        toggleDrop,
    };
},

methods: {
},
};
</script>


<style scoped>
.back-button-container {
  position: fixed;
  top: 20px;
  left: 20px;
}

.back-button {
  background: #b80404;
  color: #fff;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-weight: bold;
  transition: background-color 0.3s ease;
}

.back-button:hover {
  background: #dc3434;
}
</style>

<style scoped>
.table {
  display: flex;
  flex-direction: column;
  width: 1000px; /* Lebar tabel vertikal */
  border: 1px solid #ccc;
  border-radius: 5px;
  background: rgba(255, 255, 255, 0.9);
  margin: 0 auto;
  margin-top: 80px;
}

.table-row {
  display: flex;
  border-bottom: 1px solid #ccc;
  padding: 10px;
  justify-content: space-between;
}

.table-cell {
  flex: 1;
  padding: 5px;
}

.header {
  font-weight: bold;
}

.btn-update, .btn-delete {
  background-color: #b80505; /* Warna merah */
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 5px;
  margin-right: 5px;
}

.btn-update:hover, .btn-delete:hover {
  background-color: #ff0000; /* Warna merah yang lebih terang */
}

.heading1 {
  background-color: #b80505; /* Warna merah */
  color: #fff;
  border: none;
  background-position: center;
  width: 100%;
  position: fixed;
  top: 0; /* Menempatkan elemen di atas halaman */
  left: 0; /* Menempatkan elemen di kiri halaman */
  padding: 20px 100px;
  border-radius: 0px;
  margin-right: 0px;
  margin-bottom: 10px;
  
  
}

.background-container {
  background-image: url('logotelkom.png'); /* Ganti dengan path gambar Anda */
  background-size: 50%;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  height: 100vh; /* Mengisi seluruh tinggi tampilan layar */
}
</style>