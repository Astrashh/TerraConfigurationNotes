- {{embed ((64b322f9-0331-40ed-a030-f46963926000))}}
- Because of this limitation, any blocks attempting to generate outside of the constrained area will not work, and typically causes errors in console (however this *shouldn't* crash the game). For many placements, this will spam the console.
- In order to prevent failed attempts, you should ensure [[Structures]] placed by your feature should not generate any further than any of the adjacent (including corners) chunks.
- For features that use randomized placement, structures almost certainly will generate on the edge of chunks, meaning that there is only an additional 16 blocks of the bordering chunk horizontally for the structure to be placed without failed block placements. (There are no size limitations on the Y axis, i.e up/down)
- Based on this, it can be deduced that the safe size limitation for any structure to be placed as a feature via [[Feature Config]]s is 33x33 (16 blocks either direction + the center block).
- {{embed [[Feature Size Limit Diagram]]}}
- You can squeeze out an extra few blocks by ensuring the structure is always placed in the center of the chunk (since chunks are an even number in size, this would be a 2x2 area). Placing centrally provides a safe size limitation of 47x47 (23 blocks in either direction + the center block).
- {{embed [[Central Feature Size Limit Diagram]]}}
- The [[Overworld Config Pack]] uses this centering trick [here](https://github.com/PolyhedralDev/TerraOverworldConfig/blob/master/structures/vegetation/trees/azalea/place_great_azalea_tree_underground.tesf) for example.