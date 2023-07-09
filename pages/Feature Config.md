alias:: FEATURE

- Feature configs define the combination of:
	- A collection of [[Structures]] and
	- *Where* those structures should be placed.
- Feature configs allow you to define a placement pattern of a collection of [[Structures]], which are used inside [[BIOME]] configs.
- For example, you may have a couple tree variations in the form of [[Structures]] that you want to place in a biome called `FOREST`. A feature config would contain a list of references to these tree structures to be placed in the biome. Then you have a couple rules defined in the feature config on where these tree variations are allowed to be placed. These rules may be that the structures can only be placed in air blocks top of dirt and grass blocks
- {{embed [[Locators]]}}
- {{embed [[Distributors]]}}