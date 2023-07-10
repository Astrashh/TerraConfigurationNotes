- The `PADDED_GRID` [distributor](Distributors) segments the world into a grid of cells, and returns true for a single position within each cell. Grid cells may have padding which has the utility of preventing structures from being placed too close to each other.
- The distributor is good for use in placing
- Example config
  ```yaml
  type: FEATURE
  
  ...
  
  distributor:
    type: PADDED_GRID
    width: 6
    padding: 2
    salt: 2347 # Random number, acts like the 'seed'
    
  ...
  ```
- {{embed [[PADDED_GRID Distributor Example]]}}