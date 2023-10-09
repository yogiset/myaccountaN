<template>
  <div
    class="card custom-card"
    :class="{
      'col-12 col-md-6 col-lg-4': isGrid,
      'col-12': !isGrid
    }"
  >
    <div v-if="!isEditing">
    <img :src="karyawan.imageurl" alt="Karyawan Image" class="card-img-top" />
    <div class="card-body">
      <h5 class="card-title">Kode {{ karyawan.kodekaryawan }}</h5>
      <div class="info">
        <div class="mb-1">Nama {{ karyawan.nama }}</div>
        <div class="mb-1">Jabatan {{ karyawan.jabatan }}</div>
        <div class="mb-1">Umur {{ karyawan.umur }}</div>
        <div class="mb-1">Phone {{ karyawan.phone }}</div>
        <div class="mb-1">Email {{ karyawan.email }}</div>
        <div class="mb-1">Tanggal Lahir {{ karyawan.tgl_lahir }}</div>
        <div class="description-karyawan small text-muted"></div>
      </div>
      <button @click="editKaryawan" class="btn btn-warning">
         Edit
      </button>
      <button @click="deleteKaryawan" class="btn btn-danger">
        Delete
      </button>
    </div>
    </div>

          <!-- Display edit form when in edit mode -->
    <div v-else>
    <div class="image-upload">
  <label for="image-upload-input">
    <img v-if="editedKaryawan.imageurl" :src="editedKaryawan.imageurl" alt="Preview Image" class="img-preview" />
    <div v-else class="placeholder">
      Klik Untuk Mengupload Gambar
    </div>
  </label>
  <input id="image-upload-input" type="file" accept="image/*" @change="previewImage" />
  </div>  
    <input v-model="editedKaryawan.kodekaryawan" type="text" class="form-control" />
    <input v-model="editedKaryawan.nama" type="text" class="form-control" />
              <select v-model="editedKaryawan.jabatan" value="feature">
                <option disabled value=""> Pilih Jabatan</option>
                <option v-for="option in options.inquiry" v-bind:key="option.value">
                {{ option.text }}
                </option>
            </select>
    <input v-model="editedKaryawan.umur" type="text" class="form-control" />
    <input v-model="editedKaryawan.phone" type="text" class="form-control" />
    <input v-model="editedKaryawan.email" type="text" class="form-control" />
    <input v-model="editedKaryawan.tgl_lahir" type="date" class="form-control" />
    <button @click="saveEdit" class="btn btn-success">Save</button>
    <button @click="cancelEdit" class="btn btn-secondary">Cancel</button>  


    </div>
  </div>
</template>

<script>


export default {
props: {
karyawan: {
type: Object,
required: true,
default: 'Untitled'
},
isGrid: {
type: Boolean,
required: true,
default: false
  },
},
  data() {
    return {
      isEditing: false, // Track if the edit mode is active
      editedKaryawan: { ...this.karyawan },
            options: {

            inquiry: [
                { value: 'OfficeBoy', text: "Office Boy"},
                { value: 'KaryawanUmum', text: "Karyawan Umum"},
                { value: 'Administrasi', text: "Administrasi"},
                { value: 'Akuntan', text: "Akuntan"},
                { value: 'Manager', text: "Manager"},
                { value: 'Sekretaris', text: "Sekretaris"},
                { value: 'Direktur', text: "Direktur"},
                { value: 'Wakil Direktur', text: "Wakil Direktur"},
                { value: 'CEO', text: "CEO"},
                { value: 'Lainnya', text: "Lainnya"},
            ]
            },

    };
  },
    methods: {
    editKaryawan(){
    // Set editedKaryawan to a copy of the current karyawan
    this.editedKaryawan = { ...this.karyawan };
    // Enable edit mode
    this.isEditing = true;
    },
    deleteKaryawan(){
    // You can add a confirmation dialog here to confirm the deletion if needed
    const confirmDelete = window.confirm('Are you sure you want to delete this item?');
    
    if (confirmDelete) {
      // Delete the karyawan object (e.g., by emitting an event to notify the parent component)
      this.$emit('delete-karyawan', this.karyawan);
      }
    },
    previewImage(event) {
            const input = event.target;
            if (input.files && input.files[0]) {
            const reader = new FileReader();
            reader.onload = (e) => {
                this.editedKaryawan.imageurl = e.target.result;
            }
            reader.readAsDataURL(input.files[0]);
            }
    },
  saveEdit() {
      // Implement logic to save the edited barang to your data store or API
      // Update the original barang with edited values
    Object.assign(this.karyawan, this.editedKaryawan);
    // After saving, disable edit mode
    this.isEditing = false;
  },

  cancelEdit() {
    // If the user cancels the edit, revert the editedKaryawan object to the original karyawan
    this.editedKaryawan = { ...this.karyawan };
    // Disable edit mode
    this.isEditing = false;
  },
  
  },

computed:{

},

}
</script>
<style scoped>
.custom-card {
  width: 18rem;
}

.info {
  margin-bottom: 1rem;
}
</style>