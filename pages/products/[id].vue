<template>

  <div>

    <Head>
      <Title>Nuxt Dojo | {{ product.title }}</Title>
      <Meta name="description" :content="product.description" />
    </Head>


    <ProductDetails :product="product"/>
  </div>
</template>

<script setup>
    const { id } = useRoute().params;
    const url = `https://fakestoreapi.com/products/${id}`;

    const {data : product} = await useFetch(url,{key:id})

    if(!product.value){
        throw createError({statusCode:404,statusmessage:'Product not found', fatal:true })
    }

    definePageMeta({
        layout: 'products',
    })

    useHead({
    title: 'Nuxt Dojo | Merch',
    meta: [
      { name: 'description', content: 'Nuxt 3 Merch'}
    ]
  })
</script>

<style>

</style>