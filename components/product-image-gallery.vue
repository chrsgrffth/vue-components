<script lang="coffee">

# Usage:
# 
#   <product-image-gallery
#     :images=[
#       '/images/image1.jpg',
#       '/images/image2.jpg'
#     ]
#   ></product-image-gallery>

module.exports =
  name: "ProductImageGallery"

  data: ->
    activeImage: null

  props:
    images:
      type: Array
      required: true
  
  ready: ->
    # When the component is ready, assign the active image as the first image
    # in the images array.
    @activeImage = @images[0]

  methods:
    selectImage: (image) ->
      # Set the active image as the selected image.
      @activeImage = image

</script>

<template>

    <!-- Main/active image. -->
    <div>
      <img :src="activeImage" />
    </div>

    <!-- Thumbnails. -->
    <div>
      <div v-for="image in images" @click="selectImage(image)" :class="{ 'active': image == activeImage }">
        <img :src="image" />
      </div>
    </div>

</template>