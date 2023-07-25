<script setup>

// defineProps(['title','id','body','colorText'])

defineProps({
    title: String,
    id:Number,
     body: {
        type: String,
        default: 'Sin descripcion'
    },
 })

 const emit=defineEmits(['cambiarFavoritoNombre'])
</script>

<template>
<div class="card">
    <div class="card-body">
        <!-- <h5 class="card-title" :class="`text-${colorText}`">{{id }} - {{ title }}</h5> -->
        <h5 class="card-title">{{id }} - {{ title }}</h5>
        <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Velit quam quo consequatur ipsum inventore, iste totam beatae quidem odit ad aliquam id cum distinctio dicta porro veniam dolorum doloremque minus?</p>
        <p>{{ body }}</p>
        <button @click="emit('cambiarFavoritoNombre',title)" class="btn btn-outline-primary">Favorito</button>
    </div> 
</div>

</template>

<style></style>