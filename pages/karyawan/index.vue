<template>
<div class="py-4">
<div class="container">


<div class="title border-bottom d-flex align-items-center py-2">
<h5>Daftar karyawan</h5>



<div class="d-flex align-items-center ms-auto">
<button class="btn btn-outline-primary py-1 px-3 me-4" @click="shuffle">
Shuffle!
</button>    
<!-- /* Form input pencarian */ -->
<input type="text" class="form-control" placeholder="Cari Jabatan"
v-model="searchQuery">
<!-- /* Drop down category */ -->
<select id="akuntan" v-model="cariJabatan">
    <option value="pilih">Pilih Jabatan</option>
    <option value="OfficeBoy">OfficeBoy</option>
    <option value="KaryawanUmum">Karyawan Umum</option>
    <option value="Administrasi">Administrasi</option>
    <option value="Akuntan">Akuntan</option>
    <option value="Manager">Manager</option>
    <option value="Sekretaris">Sekretaris</option>
    <option value="Direktur">Direktur</option>
    <option value="Wakil Direktur">Wakil Direktur</option>
    <option value="CEO">CEO</option>
    <option value="Lainnya">Lainnya</option>
</select>


<div class="d-flex align-items-center justify-content-end w-100">
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
<transition-group name="karyawan" tag="div" class="list-karyawan row">
<CardKaryawan 
v-for="karyawan in filteredKaryawans"
:key="karyawan.id"
:karyawan="karyawan"
:isGrid="isGrid"
/>

</transition-group>

<form v-on:submit.prevent="handleSubmit">
<div class="action py-2">
<div class="formItem" v-for="item in karyawans" :key="item.id">{{ item.form }}</div>
<!-- /* Jika isCreating == false maka tombol Add Artikel tidak akan tampil */
/* isCreating = !isCreating berfungsi sebagai switcher toggle */ -->
<a href="#" class="add-button" v-if="!isCreating" @click.prevent="isCreating = !isCreating">Tambah Karyawan</a>
<div class="add-card" v-else>
<div class="card mb-2">
<div class="card-body d-flex flex-column p-0">
<input v-model="form.nama" class="form-control border-0 mb-2" placeholder="Nama Karyawan" type="text">
<input v-model="form.email" class="form-control border-0 mb-2" placeholder="Email" type="email">     
            <select v-model="form.jabatan" value="feature">
                <option disabled value=""> Pilih Jabatan</option>
                <option v-for="option in options.inquiry" v-bind:key="option.value">
                {{ option.text }}
                </option>
            </select>    
<input v-model="form.phone" class="form-control border-0 mb-2" placeholder="Phone Number" type="text">
<input v-model="form.tgl_lahir" class="form-control border-0 mb-2" placeholder="Tanggal Lahir" type="date">  
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
import CardKaryawan from "@/components/CardKaryawan.vue"



export default {
    
components: {
CardKaryawan
},

    data() {
        return {
            // Variabel penampung berdasar kategori
                cariJabatan: 'pilih',
            // Variabel penampung teks pencarian
                searchQuery: '',
            // Tipe layout daftar karyawans
                isGrid: false,
            // Status saat menambahkan karyawans
                isCreating: false,
            // Daftar karyawans
            form: {
                id:'',
                nama:'',
                email:'',
                jabatan:'',
                phone:'',
                tgl_lahir:'',
                imageurl:'',

            },
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

            karyawans:[
	{   
        id:1,
        kodekaryawan:"KK-22",
        nama:"Andi",
        email:"Andi@gmail.com",
        jabatan:"Karyawan Umum",
        umur:"25",
        phone:"08122345678",
        tgl_lahir:"",
		imageurl: 'https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80'
  },
	{   
        id:2,
        kodekaryawan:"KK-33",
        nama:"Ando",
        email:"Ando@gmail.com",
        jabatan:"Karyawan Umum",
        umur:"25",
        phone:"08122345677",
        tgl_lahir:"",
		imageurl: 'https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80'
  },
		{   
        id:3,
        kodekaryawan:"KK-44",
        nama:"Andu",
        email:"Andu@gmail.com",
        jabatan:"Karyawan Umum",
        umur:"24",
        phone:"08122345679",
        tgl_lahir:"",
		imageurl: 'https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80'
  },



                ],

        }
    },
        computed: {
        filteredKaryawans() {
        let filteredKaryawans = [...this.karyawans];

        if (this.searchQuery) {
            filteredKaryawans = filteredKaryawans.filter((item) =>
            this.searchQuery
                .toLowerCase()
                .split(" ")
                .every((v) => item.nama.toLowerCase().includes(v))
            );
        }

        if (this.cariJabatan !== "pilih") {
            filteredKaryawans = filteredKaryawans.filter(
            (karyawan) => karyawan.jabatan === this.cariJabatan
            );
        }

        return filteredKaryawans;
        },
    },
        methods: {
        
            shuffle() {
            this.karyawans = _.shuffle(this.karyawans)
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
            nama: this.form.nama,
            email: this.form.email,    
            jabatan: this.form.jabatan,
            phone: this.form.phone,
            tgl_lahir: this.form.tgl_lahir,
            imageurl: this.form.imageurl,
            };

            console.log('New Item:', newItem);
    
            this.karyawans.push(newItem);

            console.log('Updated Karyawans:', this.karyawans);

            // Reset the form fields after adding a karyawans
            this.form.id = '';
            this.form.nama = '';
            this.form.email = '';
            this.form.jabatan = '';
            this.form.phone = '';
            this.form.tgl_lahir = '';
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
#app .karyawan-move {
transition: .4s;
}



</style>