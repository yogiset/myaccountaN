<template>
<div
:class="[
'item-barang d-flex align-items-start border-bottom pt-3 pb-4',
isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12'
]">

<nuxt-link class="kode-barang mb-1" :to="'barang/detail/' + barang.id" >
{{ barang.kodebarang}}
</nuxt-link>
<div class="nama-barang mb-1">
{{ barang.namabarang }}
</div>
<div class="jenis-barang mb-1">
{{ barang.jenisbarang }}
</div>
<div class="jumlah-barang mb-1">
{{ barang.jumlahbarang}}
</div>
<div class="harga-barang mb-1">
{{ barang.hargabarang}}
</div>
<div class="tglmasuk mb-1">
{{ barang.tglmasuk}}
</div>
<div class="description-barang small text-muted">
<img :src="barang.imageurl" alt="Barang Image" class="img-preview barang-image" />
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