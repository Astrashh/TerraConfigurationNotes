- In previous versions of Terra (namely v5), the typical structures you'd think of such as villages, strongholds, and dungeons (not to be confused with the more generic Terra config [[Structure]]) were implemented 'in-house' i.e within packs via [[Terrascript]].
- The current latest version (as of writing, [[Version 6.3.1]]) does not have full large scale structure support, and as such compatibility with vanilla structure generation is utilized instead. This means that structures are provided via vanilla, e.g vanilla structures such as villages, strongholds, pillager outposts, etc.. will generate in Terra worlds. This further extends to any modded or otherwise structures that are implemented via the vanilla structure system, those of which should generate in Terra worlds in areas that meet the criteria determined by said structures.
- ### Feature Based Structure Placement
- The system of [[Chunkification]] and a separate structure generation stage has not been implemented yet. This means structures can only generate within the [[Feature Generation Stages]] .
- [[Structure]]s generated within the [[Feature Generation Stages]] are limited to generating within the chunk of origin as well as any of the 8 bordering chunks, i.e a 3x3 chunk area centered on the chunk the origin of the structure generates in.
  id:: 64b322f9-0331-40ed-a030-f46963926000
- You can still implement what would be considered a typical structure via the [[Feature Generation Stages]] using [[Feature Config]]s, however keep in mind the 3x3 chunk limitation. Also see: [[Working with feature size limits]].