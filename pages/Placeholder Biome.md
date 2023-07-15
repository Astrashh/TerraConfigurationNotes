- Placeholder biomes are special names used in the [[Pipeline Biome Provider]] as stand-ins for real biome IDs.
- Placeholder biomes are created simply by declaring a [[String]] that is not a valid biome ID anywhere a [[Pipeline Biome]] is accepted. As a convention, placeholder biomes should be defined in all lowercase with hyphens in place of spaces to easily distinguish them from biome IDs which are all uppercase.
- The main use case for placeholder biomes is when you wish to use labels to distribute a particular area or pattern rather than real biomes. In the [[Overworld Config Pack]], placeholder biomes are used to distribute climate areas which are then later replaced with real biomes.
- This is useful for organization of zones to be manipulated by pipeline stages, as using the placeholder as a label for a zone makes it clear what that zone between stages is supposed to be. Rather than for example using a `PLAINS` biome as meaning 'temperate zone', placeholder biomes simply let you define a `temperate` label that would act as though you were distributing a regular biome.
- A pipeline config will fail to load if it is possible for a placeholder biome to end up in the final biome placement, this is called a 'pipeline leak'.  To prevent a pipeline leak you must ensure all placeholder biomes follow a replacement chain that results in a real biome.
	- E.g this would not load because `placeholder-biome` is in the list of final biomes that could potentially generate because it has not been replaced with a real biome:
	  ```yaml
	  ... 
	  
	  source:
	    type: SAMPLER
	    biomes:
	      - placeholder-biome: 1
	      - PLAINS: 1
	    sampler:
	      ...
	  stages: [] # No stages
	  
	  ...
	  ```
	- If we however replace `placeholder-biome` with a real biome using for example a `REPLACE` stage, then the pipeline would be valid:
	  ```yaml
	  ... 
	  
	  source:
	    type: SAMPLER
	    biomes:
	      - placeholder-biome: 1
	      - PLAINS: 1
	    sampler:
	      ...
	  stages:
	    - type: REPLACE
	      from: placeholder-biome
	      to: FOREST
	  
	  ...
	  ```
-