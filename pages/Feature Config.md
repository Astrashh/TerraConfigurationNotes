alias:: FEATURE

- Feature configs define the combination of:
	- A collection of [[Structures]] and
	- *Where* those structures should be placed.
- Feature configs allow you to define a placement pattern of a collection of [[Structures]], which are used inside [[BIOME]] configs.
- For example, you may have a couple of tree structure variations and you want to place these tree structures in a biome. A feature config would contain this list of references to these tree structures to be placed in the biome. Then you have a couple rules defined in the feature config on where these tree variations are allowed to be placed. These rules may be that the structures can only be placed in air blocks that are on top of dirt and grass blocks, and that the structures should be placed in a grid-like fashion.
- Each of these things are defined by three sub-configurations:
	- [[Feature Structure List]]
	- [[Locators]]
	- [[Distributors]]
- The
- {{embed [[Feature Structure List]]}}
- {{embed [[Locators]]}}
- {{embed [[Distributors]]}}