<template>
<div
:class="[
'item-karyawan d-flex align-items-start border-bottom pt-3 pb-4',
isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12'
]">

<nuxt-link class="kode-karyawan mb-1" :to="'karyawan/detail/' + karyawan.id" >
{{ karyawan.kodekaryawan }}
</nuxt-link>
<div class="nama mb-1">
{{ karyawan.nama }}
</div>
<div class="jabatan mb-1">
{{ karyawan.jabatan }}
</div>
<div class="umur mb-1">
{{ karyawan.umur }}
</div>
<div class="phone mb-1">
{{ karyawan.phone }}
</div>
<div class="email mb-1">
{{ karyawan.email }}
</div>
<div class="tgl_lahir mb-1">
{{ karyawan.tgl_lahir }}
</div>
<div class="description-karyawan small text-muted">
<img :src="karyawan.imageurl" alt="Karyawan Image" class="img-preview karyawan-image" />
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
}
,
default(){
    return{}
}
},
computed:{

}

}
</script>
<style>


</style>