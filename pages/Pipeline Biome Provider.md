- 'The pipeline' is a [[Biome Provider]] that distributes biomes procedurally in 2D.
  {{embed [[Biome Provider]] }}
- The pipeline biome provider is implemented by the `biome-provider-pipeline-v2` [[Addon]] and uses the `PIPELINE` key which should be defined as the biome provider `type`, make sure to [add the addon as a dependency](How to add an addon as a dependency) if you wish to use it.
- The name pipeline comes from the way it is configured, there is a *source* produces an initial biome layout, which then gets passed through a set of *stages* that each provide successive modifications to the biome layout.
- {{embed [[Pipeline Diagram]]}}
- The config contains a handful of top level [[config key]]s:
	- `resolution` - Optional, the quality at which the pipeline samples at. Higher resolutions = larger samples = lower quality = faster generation.
		- At a resolution of 4, each sample would be 4x4 blocks.
		- Higher resolutions will result in blocky looking biome placement.
		- A resolution of 4 is recommended as a good balance between being performant and not looking as obvious as higher resolutions.
		- Example:
		  ```yaml
		  biomes:
		    type: PIPELINE
		  ...
		    resolution: 4
		  ...
		  ```
	- `blend` - Optional, warps the biome distribution, with the purpose of blending hard edges produced by increased resolutions.
		- The blend [[config key]] allows for fuzzing the hard edges of blocky looking samples and contains two subkeys:
		- `amplitude` - A [[Float]] that determines the strength of the blending.
		- `sampler` - A [[Noise Sampler]] that determines what the warping pattern is.
		- Example:
		  ```yaml
		  biomes:
		    type: PIPELINE
		  ...
		    blend:
		      amplitude: 1.5
		      sampler:
		        type: WHITE_NOISE
		  ...
		  ```
	- `pipeline` - Contains two subkeys that define the *source* and *stages*:
		- `source`
			- {{embed [[Pipeline Source]]}}
			- In the context of a pipeline config, this would be configured as
			  ```yaml
			  biomes:
			    type: PIPELINE
			  ...
			    pipeline:
			  ...
			      source:
			        type: SAMPLER
			        biomes:
			          FOREST: 3
			          OCEAN: 2
			        sampler:
			          type: OPEN_SIMPLEX_2
			          frequency: 0.01
			  ...
			  ```
		- `stages` - A list of [[Pipeline Stage]]s that each make some kind of modification
			- {{embed [[Pipeline Stage]]}}
			- Example of a couple of stages configured, which make rare variants of biomes generate:
			  ```yaml
			  biomes:
			    type: PIPELINE
			  ...
			    pipeline:
			  ...
			      stages:
			        - type: REPLACE
			          from: PLAINS
			          to: 
			            - SELF: 10
			            - SUNFLOWER_PLAINS: 1
			          sampler:
			            type: CELLULAR
			            frequency: 0.01
			            salt: 1
			            
			        - type: REPLACE
			          from: FOREST
			          to:
			            - SELF: 10
			            - FLOWER_FOREST: 1
			          sampler:
			            type: CELLULAR
			            frequency: 0.01
			            salt: 2
			  ...
			  ```
- Here is an example of a simple pipeline setup which generates a mix of plains and forest, as well as some rare variants of those biomes, this would go in the [[Config Pack Manifest]] :
  ```yaml
  id: MY_PACK
  
  ...
  
  biomes:
    type: PIPELINE
    resolution: 4
    blend:
      amplitude: 1.5
      sampler:
        type: WHITE_NOISE
    pipeline:
      source:
        type: SAMPLER
        biomes:
          - PLAINS: 1
          - FOREST: 1
        sampler:
          type: OPEN_SIMPLEX_2
          frequency: 0.005
      stages:
        - type: REPLACE
          from: PLAINS
          to: 
            - SELF: 10
            - SUNFLOWER_PLAINS: 1
          sampler:
            type: CELLULAR
            frequency: 0.01
            salt: 1
            
        - type: REPLACE
          from: FOREST
          to:
            - SELF: 10
            - FLOWER_FOREST: 1
          sampler:
            type: CELLULAR
            frequency: 0.01
            salt: 2
  
  ...
  ```
-