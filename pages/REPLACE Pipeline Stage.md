- Replaces a [[Pipeline Biome]] with a [[Weighted Pool]] of pipeline biomes according to a [[Noise Sampler]]. This is a similar process to the [[SAMPLER Pipeline Source]].
- Example:
  ```yaml
  type: REPLACE
  from: FOREST
  to:
    - FOREST_DENSE: 1
    - FLOWER_FOREST: 1
    - SELF: 10 # A convenience keyword that replaces with the pipeline biome being replaced,
            # e.g this would be equivalent to using FOREST here
  sampler:
    type: CELLULAR
    frequency: 0.01
    return: CellValue
  ```
- The example would replace all instances of the `FOREST` [[Pipeline Biome]] with occasional patches of `FOREST_DENSE` and `FLOWER_FOREST`.