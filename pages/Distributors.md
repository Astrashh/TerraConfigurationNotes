- Distributors are defined in [[FEATURE]] configs under the `distributor` [[config key]].
- Distributors determine which columns in the world the structures can be placed in / which columns [[Locators]] should operate in.
- Distributors operate in 2D. For each set of 2D coordinates within the biome, a distributor will return either *true* or *false*, where true means the locator will be applied for the column of blocks to determine where a [[Structure]] can generate.
- {{embed [[Distributor Diagram]]}}
- A distributor is defined inside a [[FEATURE]] config like so:
  ```yaml
  distributor:
    type: ...
  ```
  where the distributor config is indented in-line with the `type` key.
- Use the `type` key to choose which distributor to use in your [[FEATURE]] config.
- There are several distributors to choose from, each determining which columns to place features in differently.
- Here is one example of a distributor:
- {{embed [[PADDED_GRID Distributor]]}}
- {{embed [[Distributor List]]}}