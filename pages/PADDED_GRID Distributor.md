- The `PADDED_GRID` [[Distributors]]
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