- How terrain generates comes from the [[Chunk Generator]]. Currently there is just the `NOISE_3D` chunk generator which is provided by the `chunk-generator-noise-3d` [[Core Addon]], so this page will focus on working with that.
- {{embed [[Chunk Generator]]}}
- The chunk generator should already be set if you're working with a pack that can load, setting it in your [[Pack Manifest]] should look like this:
  ```yaml
  id: MY_CONFIG_PACK
  ...
  generator: NOISE_3D
  ...
  ```
- `NOISE_3D` requires each [[Biome Config]] to specify how the terrain should be shaped. This is configured via the `terrain.sampler` [[config parameter]], which is a 3D [[Noise Sampler]], and must be defined for a biome config for it to be valid.
- Here is the skeleton of a config with `terrain.sampler` defined:
  ```yaml
  id: COOL_BIOME
  type: BIOME
  ...
  terrain:
    sampler:
      # 3D noise sampler goes here
  ```
- ### How the terrain parameters control terrain shaping
- Each block can either be 'solid' or 'air'. The *simplified model* of how a block is determined to be either solid or air is as follows:
- The position of the block is sampled by the block's biome's `terrain.sampler`. The value of this sample is considered the block's 'density'.
  logseq.order-list-type:: number
- If the block's density is greater than 0 (i.e. any positive number), then it is considered solid, and if not (i.e. any negative number and zero), it is considered air.
  logseq.order-list-type:: number
- logseq.order-list-type:: number
- Based on this, we can make every block solid in a biome by using a [[Noise Sampler]] which always outputs a positive number:
  ```yaml
  # Set every block to solid
  terrain:
    sampler: # This noise sampler always outputs a constant value of 1
      type: CONSTANT
      value: 1
  ```
- Alternatively we could make every block air in a biome by using a negative value or 0:
  ```yaml
  # Set every block to air
  terrain:
    sampler:
      type: CONSTANT
      value: -1
  ```
- Try out some of the samplers listed [here](http://terra.polydev.org/config/documentation/sampler/index.html) and see what results you get. Below are some examples. Try and figure out why they produce the results they do:
- ```yaml
  terrain:
    sampler:
      type: OPEN_SIMPLEX_2
  ```\
- ```yaml
  terrain:
    sampler:
      type: FBM
      sampler:
        type: OPEN_SIMPLEX_2
  ```
- ```yaml
  terrain:
    sampler:
      type: WHITE_NOISE
  ```
- To create flat terrain we will need to:
	- Produce positive values (=solid) *below* a certain y level
	- Produce negative values (=air) *above* that y level
- The simplest way to do this is by outputting the negative y level, resulting in positive values below y=0, and negative values above y=0.
- This can be done using the [[EXPRESSION]] [[Noise Sampler]] like so:
  ```yaml
  terrain:
    sampler:
      type: EXPRESSION
      expression: -y
  ```
  
  Here is a visual for the density at each y level:
  ![image.png](../assets/image_1691900504307_0.png){:height 248, :width 356}
- If we then add 1 to the density, we will in effect shift the terrain upwards by 1 block:
  ```yaml
  terrain:
    sampler:
      type: EXPRESSION
      expression: -y + 1
  ```
  
  Here is the same set of block positions, note that each number from the previous example has +1 added to it, and therefore the terrain has shifted above the blue line by 1 block.
  ![image.png](../assets/image_1691900686655_0.png){:height 248, :width 356}
- Based on this, we can deduce that the number added to `-y` will correspond to the height of the terrain. For example for flat terrain at y=64, you could use this:
  ```yaml
  terrain:
    sampler:
      type: EXPRESSION
      expression: -y + 64
  ```
- We can make a general formula `-y + h` where `h` = terrain height.