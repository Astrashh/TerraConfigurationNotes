- Base image related functionality is introduced by the `library-image` addon, [add that as a dependency](How to add an addon as a dependency) to get started working with images.
- You can find the official documentation for image related functionality [here](https://terra.polydev.org/config/documentation/image/index.html).
- ## Distributing biomes using an image
- The most basic method of distributing biomes via image(s) is by utilizing the `IMAGE` [[Biome Provider]] which is implemented by the `biome-provider-image-v2` addon. Make sure you [add that as a dependency](How to add an addon as a dependency) before continuing.
- {{embed [[Biome Provider]]}}
- Set the `type` key to `IMAGE`.
- The skeleton of the image biome provider looks like so:
  ```yaml
  id: MY_CONFIG_PACK
  
  ...
  
  biomes:
    type: IMAGE
    
    color-sampler:
      ...
     
    color-conversion:
      ...
  
  ...
  ```
	- `color-sampler` - a [[Color Sampler]] config.
	- `color-conversion` - A [[Color Converter]] that maps colors to biomes.
- Example config:
  ```yaml
  id: MY_CONFIG_PACK
  
  ...
  
  biomes:
    type: IMAGE
    color-sampler:
      type: SINGLE_IMAGE # Only gen a single image rather tiling
      align: CENTER # Makes center of image at 0,0
      image:
        type: BITMAP
        path: images/biome.png
      outside-sampler: # What to use outside the image
        type: COLOR
        color: "#0000FF" # Use blue for area outside the image
    color-conversion:
      type: CLOSEST # Pick the biome based on the most similar color in the image
      match:
        type: USE_BIOME_COLORS # Use the 'color' key in biome configs
                               # as each biome's color
        
  ...
  ```
- Modified example that moves where the center of the image is:
  ```yaml
  id: MY_CONFIG_PACK
  
  ...
  
  biomes:
    type: IMAGE
    color-sampler:
      type: TRANSLATE # Translates an image sampler center to 500,-500
      x: 500
      y: -500
      color-sampler: # Color sampler to be translated
        type: SINGLE_IMAGE # Only gen a single image rather tiling
        align: CENTER # Makes center of image at 0,0
        image:
          type: BITMAP
          path: images/biome.png
        outside-sampler: # What to use outside the image
          type: COLOR
          color: "#0000FF" # Use blue for area outside the image
    color-conversion:
      type: CLOSEST # Pick the biome based on the most similar color in the image
      match:
        type: USE_BIOME_COLORS # Use the 'color' key in biome configs
                               # as each biome's color
        
  ...
  ```
- Another modified example that uses a manually defined biome color mapping:
  ```yaml
  id: MY_CONFIG_PACK
  
  ...
  
  biomes:
    type: IMAGE
    color-sampler:
      type: SINGLE_IMAGE # Only gen a single image rather tiling
      align: CENTER # Makes center of image at 0,0
      image:
        type: BITMAP
        path: images/biome.png
      outside-sampler: # What to use outside the image
        type: COLOR
        color: "#0000FF" # Use blue for area outside the image
    color-conversion:
      type: CLOSEST # Pick the biome based on the most similar color in the image
      match:
        type: MAP
        map:
          "#00FF00": PLAINS # Green pixels will map to plains
          "#FF0000": DESERT # Red pixels will map to desert
          "#0000FF": OCEAN # Blue pixels will map to ocean, since this is the 
                           # same as the color the 'outside-sampler' produces,
                           # everywhere outside the image will be ocean.
  
  ...
  ```