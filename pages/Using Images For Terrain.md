- Example of an abstract [[Biome Config]] configured to generate terrain based on a grayscale heightmap image. See also: [[Shaping Terrain]] 
  
  ```yaml
  id: TERRAIN_IMAGE
  type: BIOME
  abstract: true
  
  variables: &variables
    base: 64 # Base height where grayscale value of the image = 0
    height: 100 # Height of the terrain where grayscale value of the image = 255
  
  terrain:
    sampler:
      type: EXPRESSION
      expression: -y + base
      variables: *variables
        
    sampler-2d:
      type: EXPRESSION
      expression: image(x, z) * height
      variables: *variables
      samplers:
        image:
          dimensions: 2
          type: PROBABILITY
          sampler:
            type: CHANNEL
            channel: GRAYSCALE # Other options are RED, GREEN, BLUE, and ALPHA
            color-sampler:
              type: SINGLE_IMAGE # Only use a single image rather tiling infinitely
              align: CENTER # Makes center of image at 0,0
              image:
                type: BITMAP
                path: images/heightmap.png # Path to the image within your config pack
              outside-sampler:
                type: COLOR
                color: "#000000" # Use black for area outside the image
  
  ```
- To apply this to a [[Biome Config]], set the `extends` [[config parameter]] to include `TERRAIN_IMAGE` like so:
  ```yaml
  id: MY_BIOME
  type: BIOME
  extends:
    - TERRAIN_IMAGE
  ```