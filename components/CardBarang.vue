<template>
  <div
    class="card custom-card"
    :class="{
      'col-12 col-md-6 col-lg-4': isGrid,
      'col-12': !isGrid
    }"
  >
    <div v-if="!isEditing">
    <img :src="barang.imageurl" alt="Barang Image" class="img-preview barang-image" />
    <div class="card-body">
      <h5 class="card-title">{{ barang.kodebarang }}</h5>
      <div class="info">
        <div class="mb-1 nama-barang">Nama {{ barang.namabarang }}</div>
        <div class="mb-1 jenis-barang">Jenis {{ barang.jenisbarang }}</div>
        <div class="mb-1 jumlah-barang">Jumlah {{ barang.jumlahbarang }}</div>
        <div class="mb-1 harga-barang">Harga {{ barang.hargabarang }}</div>
        <div class="mb-1 tglmasuk">Tanggal Masuk {{ barang.tglmasuk }}</div>
        <div class="description-barang small text-muted"></div>
      </div>
      <button @click="editBarang" class="btn btn-warning">
        Edit
      </button>
      <button @click="deleteBarang" class="btn btn-danger">
       Delete
      </button>
    </div>
    </div>

    <!-- Display edit form when in edit mode -->
    <div v-else>
    <div class="image-upload">
  <label for="image-upload-input">
    <img v-if="editedBarang.imageurl" :src="editedBarang.imageurl" alt="Preview Image" class="img-preview" />
    <div v-else class="placeholder">
      Klik Untuk Mengupload Gambar
    </div>
  </label>
  <input id="image-upload-input" type="file" accept="image/*" @change="previewImage" />
  </div>  
    <input v-model="editedBarang.kodebarang" type="text" class="form-control" />
    <input v-model="editedBarang.namabarang" type="text" class="form-control" />
              <select v-model="editedBarang.jenisbarang" value="feature">
                <option disabled value=""> Pilih Jenis Barang</option>
                <option v-for="option in options.inquiry" v-bind:key="option.value">
                {{ option.text }}
                </option>
            </select>
    <input v-model="editedBarang.jumlahbarang" type="text" class="form-control" />
    <input v-model="editedBarang.hargabarang" type="text" class="form-control" />
    <input v-model="editedBarang.tglmasuk" type="date" class="form-control" />
    <button @click="saveEdit" class="btn btn-success">Save</button>
    <button @click="cancelEdit" class="btn btn-secondary">Cancel</button>  

  </div>
  </div>
</template>

<script>
export default {
  props: {
    barang: {
      type: Object,
      required: true,
      default: 'Untitled'
    },
    isGrid: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  data() {
    return {
      isEditing: false, // Track if the edit mode is active
      editedBarang: { ...this.barang },// Initialize editedBarang with the current barang
      options: {
            inquiry: [
                { value: 'Laptop', text: "Laptop"},
                { value: 'PC', text: "PC"},
                { value: 'Monitor', text: "Monitor"},
                { value: 'Mobil', text: "Mobil"},
                { value: 'Motor', text: "Motor"},
                { value: 'Lainnya', text: "Lainnya"},
            ]
            },

    };
  },
  methods: {
    editBarang(){
    // Set editedBarang to a copy of the current barang
    this.editedBarang = { ...this.barang };
    // Enable edit mode
    this.isEditing = true;
    },
    deleteBarang(){
    // You can add a confirmation dialog here to confirm the deletion if needed
    const confirmDelete = window.confirm('Are you sure you want to delete this item?');
    
    if (confirmDelete) {
      // Delete the barang object (e.g., by emitting an event to notify the parent component)
      this.$emit('delete-barang', this.barang);
      }
    },
    previewImage(event) {
            const input = event.target;
            if (input.files && input.files[0]) {
            const reader = new FileReader();
            reader.onload = (e) => {
                this.editedBarang.imageurl = e.target.result;
            }
            reader.readAsDataURL(input.files[0]);
            }
    },
  saveEdit() {
      // Implement logic to save the edited barang to your data store or API
      // Update the original barang with edited values
    Object.assign(this.barang, this.editedBarang);
    // After saving, disable edit mode
    this.isEditing = false;
  },

  cancelEdit() {
    // If the user cancels the edit, revert the editedBarang object to the original barang
    this.editedBarang = { ...this.barang };
    // Disable edit mode
    this.isEditing = false;
  },
  
  },
};
</script>

<style scoped>
.custom-card {
  width: 18rem;
}

.info {
  margin-bottom: 1rem;
}

.nama-barang,
.jenis-barang,
.jumlah-barang,
.harga-barang,
.tglmasuk {
  margin-bottom: 1rem;
}

</style>