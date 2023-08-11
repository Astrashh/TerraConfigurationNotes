- Terra world generation happens in several distinct [[Generation Stages]]. Feature generation stages are a set of these world gen stages that occur after the [[Chunk Generator]] has created the initial terrain.
- Feature generations stages are when [[Feature Config]]s are applied to the world.
- You can define feature generation stages in the [[Config Pack Manifest]] like so:
  ```yaml
  ...
  
  id: MY_COOL_CONFIG_PACK
  
  ...
  
  stages:
    - id: the-first-feature-stage
      type: FEATURE
      
    - id: another-feature-stage
      type: FEATURE
  ```
- The stages defined here will generate sequentially, meaning `the-first-feature-stage` will be applied first, then `another-feature-stage` will apply second.
- After defining these feature stages, you can add [[Feature Config]]s to stages in each [[Biome Config]]s by listing them under the `features` [[config key]] like so:
  ```yaml
  ...
  
  id: MY_EPIC_BIOME
  
  ...
  
  features:
    the-first-feature-stage:
      - MY_COOL_FEATURE
      - MY_OTHER_COOL_FEATURE
    another-feature-stage:
      - ANOTHER_FEATURE
  ...
  
  ```
- [[Biome Config]]s do not have to have features for every feature stage:
  ```yaml
  ...
  
  id: MY_EPIC_BIOME
  
  ...
  
  features:
    another-feature-stage:
      - MY_COOL_FEATURE
      
  ...
  
  ```
- Ordering of feature generation stages is determined by how they are defined in the [[Config Pack Manifest]], so it does not matter how you order them inside your [[Biome Config]]s.
- If features should generate in a certain order, they should be placed in separate stages, as ordering of features within the same stage does not reflect generation order.
- When it comes to [[Config Inheritance]], note that each stage in a [[Biome Config]] is considered a separate parameter, e.g. the stages defined above would add two separate parameters `features.the-first-feature-stage` and `features.another-feature-stage` rather than one singular parameter `features`.
	- For example for the following configs:
	  ```yaml
	  id: PARENT
	  type: BIOME
	  abstract: true
	  features:
	    the-first-feature-stage:
	      - FEATURE_A
	    another-feature-stage:
	      - FEATURE_B
	  ```
	  
	  ```yaml
	  id: CHILD
	  type: BIOME
	  extends:
	    - PARENT
	  
	  ...
	  
	  features:
	    another-feature-stage:
	      - FEATURE_C
	  ```
	  
	  The config `CHILD` will inherit `FEATURE_A` generating in `the-first-feature-stage` from `PARENT`:
	  ```yaml
	  features:
	    the-first-feature-stage:
	      - FEATURE_A
	  ```
	  And override `PARENT`'s definition of `FEATURE_B` in `another-feature-stage` with its own definition of `FEATURE_C` in `another-feature-stage`, meaning `CHILD` will in effect have:
	  ```yaml
	  features:
	    the-first-feature-stage:
	      - FEATURE_A
	    another-feature-stage:
	      - FEATURE_C
	  ```
	- This is useful because it allows you to define sets of features for a particular feature stage in an abstract biome, then make several biome configs use that same set of features via `extends`.
-