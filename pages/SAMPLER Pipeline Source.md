- Distributes a [[Weighted Pool]] of [[Pipeline Biome]]s according to a [[Noise Sampler]]. See the official docs on [noise segmentation](https://terra.polydev.org/config/development/samplers/index.html#noise-segmentation) to understand how this process works.
- Contains two subkeys:
	- `sampler` - The [[Noise Sampler]] used to distribute the biomes
	- `biomes` - A weighted pool of [[Pipeline Biome]]s
- Example:
  ```yaml
  type: SAMPLER
  biomes:
    - FOREST: 3
    - OCEAN: 2
  sampler:
    type: OPEN_SIMPLEX_2
    frequency: 0.01
  ```