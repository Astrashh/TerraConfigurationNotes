- A chunk generator provides functionality for generating the initial state for any given chunk. You can think of this as providing the 'foundation' of a chunk before any further decoration has been applied.
- This typically includes creating the terrain shape as well as the blocks that the terrain is composed of.
- The chunk generator a config pack will use is set in the [[Pack Manifest]] under the `generator` [[config parameter]].
  id:: 64d83f2b-31c3-4529-9094-5782f4f2cd9e