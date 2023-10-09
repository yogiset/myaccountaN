<template>
<div class="py-4">
<div class="container">


<div class="title border-bottom d-flex align-items-center py-2">
<h5>Inventaris</h5>



<div class="d-flex align-items-center ms-auto">   
<!-- /* Form input pencarian */ -->
<input type="text" class="form-control search-input" placeholder="Cari"
v-model="searchQuery">
<!-- /* Drop down category */ -->
<select id="akuntan" class="form-control category-dropdown" v-model="cariJenis">
    <option value="pilih">Pilih Jenis Barang</option>
    <option value="Laptop">Laptop</option>
    <option value="PC">PC</option>
    <option value="Monitor">Monitor</option>
    <option value="Mobil">Mobil</option>
    <option value="Motor">Motor</option>
    <option value="Lainnya">Lainnya</option>
</select>


<div class="d-flex align-items-center justify-content-end w-100 view-as-button">
<span class="me-2">View As</span>
<button
class="btn btn-outline-secondary py-1 px-3"
@click="isGrid = !isGrid"
>
{{ isGrid ? 'Grid' : 'List' }}
</button>
</div>
</div>
</div>
<transition-group name="barang" tag="div" class="list-barang row">
<CardBarang 
v-for="barang in filteredBarangs"
:key="barang.id"
:barang="barang"
:isGrid="isGrid"
@delete-barang="handleDeleteBarang"
/>

</transition-group>

<form v-on:submit.prevent="handleSubmit">
<div class="action py-2">
<div class="formItem" v-for="item in barangs" :key="item.id">{{ item.form }}</div>
<!-- /* Jika isCreating == false maka tombol Add Artikel tidak akan tampil */
/* isCreating = !isCreating berfungsi sebagai switcher toggle */ -->
<a href="#" class="add-button" v-if="!isCreating" @click.prevent="isCreating = !isCreating">Tambah Barang</a>
<div class="add-card" v-else>
<div class="card mb-2">
<div class="card-body d-flex flex-column p-0">
<input v-model="form.namabarang" class="form-control border-0 mb-2" placeholder="Nama Barang" type="text">    
            <select v-model="form.jenisbarang" value="feature">
                <option disabled value=""> Pilih Jenis Barang</option>
                <option v-for="option in options.inquiry" v-bind:key="option.value">
                {{ option.text }}
                </option>
            </select>    
<input v-model="form.jumlahbarang" class="form-control border-0 mb-2" placeholder="Jumlah Barang" type="text">
<input v-model="form.hargabarang" class="form-control border-0 mb-2" placeholder="harga Barang" type="text">
<input v-model="form.tglmasuk" class="form-control border-0 mb-2" placeholder="Tanggal Masuk" type="date">  
<div class="image-upload">
  <label for="image-upload-input">
    <img v-if="form.imageurl" :src="form.imageurl" alt="Preview Image" class="img-preview" />
    <div v-else class="placeholder">
      Klik Untuk Mengupload Gambar
    </div>
  </label>
  <input id="image-upload-input" type="file" accept="image/*" @change="previewImage" />
</div>

</div>
</div>
<div class="button-wrapper d-flex">
<button class="btn btn-primary me-2" type="submit">save</button>
<button class="btn btn-outline-secondary" @click="isCreating =
!isCreating">Cancel</button>
</div>
</div>
</div>
</form>




</div>
</div>
</template>
<script>
import CardBarang from "@/components/CardBarang.vue"



export default {
    
components: {
CardBarang
},

    data() {
        return {
            // Variabel penampung berdasar kategori
                cariJenis: 'pilih',
            // Variabel penampung teks pencarian
                searchQuery: '',
            // Tipe layout daftar barangs
                isGrid: false,
            // Status saat menambahkan barangs
                isCreating: false,
            // Daftar barangs
            form: {
                id:'',
                namabarang:'',
                jenisbarang:'',
                jumlahbarang:'',
                hargabarang:'',
                tglmasuk:'',
                imageurl:'',

            },
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

            barangs:[
	{   
        id:1,
        kodebarang:"LP-22",
        namabarang:"laptop 1",
        jenisbarang:"Laptop",
        jumlahbarang :"100",
        hargabarang:"10000",
        tglmasuk:"",
		imageurl: 'https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80'
  },
	{   
        id:2,
        kodebarang:"LP-11",
        namabarang:"laptop 2",
        jenisbarang:"Laptop",
        jumlahbarang :"100",
        hargabarang:"10000",
        tglmasuk:"",
		imageurl: 'https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80'
  },
	{   
        id:3,
        kodebarang:"LP-33",
        namabarang:"laptop 3",
        jenisbarang:"Laptop",
        jumlahbarang :"100",
        hargabarang:"10000",
        tglmasuk:"",
		imageurl: 'https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80'
  },



                ],

        }
    },
        computed: {
        filteredBarangs() {
        let filteredBarangs = [...this.barangs];

        if (this.searchQuery) {
            filteredBarangs = filteredBarangs.filter((item) =>
            this.searchQuery
                .toLowerCase()
                .split(" ")
                .every((v) => item.namabarang.toLowerCase().includes(v))
            );
        }

        if (this.cariJenis !== "pilih") {
            filteredBarangs = filteredBarangs.filter(
            (barang) => barang.jenisbarang === this.cariJenis
            );
        }

        return filteredBarangs;
        },
    },
        methods: {
    handleDeleteBarang(deletedBarang) {
    // Find the index of the deletedBarang in your data array
    const index = this.barangs.findIndex((barang) => barang.id === deletedBarang.id);

    if (index !== -1) {
      // Remove the deletedBarang from the data array
      this.barangs.splice(index, 1);
    }
      },

          previewImage(event) {
            const input = event.target;
            if (input.files && input.files[0]) {
            const reader = new FileReader();
            reader.onload = (e) => {
                this.form.imageurl = e.target.result;
            }
            reader.readAsDataURL(input.files[0]);
            }
    },


        handleSubmit() {
            const newItem = {
            id: this.form.id,
            namabarang: this.form.namabarang,
            jenisbarang: this.form.jenisbarang,    
            jumlahbarang: this.form.jumlahbarang,
            hargabarang: this.form.hargabarang,
            tglmasuk: this.form.tglmasuk,
            imageurl: this.form.imageurl,
            };

            console.log('New Item:', newItem);
    
            this.barangs.push(newItem);

            console.log('Updated Barangs:', this.barangs);

            // Reset the form fields after adding a barangs
            this.form.id = '';
            this.form.namabarang = '';
            this.form.jenisbarang = '';
            this.form.jumlahbarang = '';
            this.form.hargabarang = '';
            this.form.tglmasuk = '';
            this.form.imageurl = '';
        }
    },      
            

}   














</script>

<style>
select {
  background-color: #fff;
  border: 1px solid #ccc;
  padding: 10px;

}

select option {
  padding: 5px;
}
#app .barang-move {
transition: .4s;
}

/* Container for search, category, and "View As" bars */
.search-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

/* Search input */
.search-input {
  flex-grow: 1;
  margin-right: 1rem;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

/* Category dropdown */
.category-dropdown {
  flex-basis: 70%;
  margin-right: 1rem;
}

/* "View As" button */
.view-as-button {
  margin-left: auto;
}

/* Style the category dropdown options */
.category-dropdown select {
  background-color: #fff;
  border: 1px solid #ccc;
  padding: 10px;
  width: 100%;
}

/* Style the "View As" button */
.view-as-button button {
  padding: 0.5rem 1rem;
  font-weight: bold;
}

/* Style the "View As" button text */
.view-as-button span {
  margin-right: 0.5rem;
  font-size: 14px;
}

/* Align the "View As" button to the right */
.view-as-button {
  margin-left: auto;
}

</style>