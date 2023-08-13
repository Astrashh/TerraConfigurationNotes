- A biome provider is a configuration that determines how / where biomes get placed in the world.
- Each config pack has a singular main biome provider which is defined under the `biomes` [[config parameter]] like so:
  ```yaml
  id: MY_CONFIG_PACK
  
  ...
  
  biomes:
    type: # Which biome provider to use
    # Rest of biome provider configuration
  ...
  ```