- Locators determine how features are placed on the Y axis.
- Locators are defined in [[FEATURE]] configs under the `locator` key.
- ```yaml
  locator:
    type: ...
  ```
- Use the `type` key to choose which locator to use in your [[FEATURE]] config.
- There are several locator types to choose from, each with different behaviors that determine how your feature should be placed on the Y axis.
- Locators are implemented in the `config-locators` [[Core Addon]], make sure to add this as an addon dependency () you can find the source code for https://github.com/PolyhedralDev/Terra/tree/master/common/addons/config-locators/src/main/java/com/dfsek/terra/addons/feature/locator