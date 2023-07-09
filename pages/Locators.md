- Locators determine *where* features are placed on the Y axis.
- Locators are defined in [[FEATURE]] configs under the `locator` key.
- Locators iterate through each block within a column of blocks in the world (typically within a constrained Y level range defined by the locator config), and return either *true* or *false*, signifying if the feature's structure should generate at that position or not. True means that a structure will be placed at that block, and vice-versa for false.
- Locators are defined inside the [[FEATURE]] config like so:
  ```yaml
  locator:
    type: ...
  ```
  where the locator config is indented in-line with the `type` key.
- Use the `type` key to choose which locator to use in your [[FEATURE]] config.
- There are several locator types to choose from, each with different behaviors that determine how your feature should be placed on the Y axis.
- Here is one example of a locator:
- {{embed [[SURFACE Locator]]}}
- {{embed [[Documented Locators]]}}
- Locators are implemented in the `config-locators` [[Core Addon]], make sure to add this as an addon dependency ([?](How to add an addon as a dependency)). You can find the source code for the addon here: https://github.com/PolyhedralDev/Terra/tree/master/common/addons/config-locators/