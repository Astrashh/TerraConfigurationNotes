- [Open `pack.yml`](How to find your pack manifest)
  logseq.order-list-type:: number
- Look for the [key](Config Keys) called `addons`
  logseq.order-list-type:: number
- Add your addon under the `addons` key, the format is a key-value pairing of the [[Addon]] name, and the [[Semver Pattern Match]]
  logseq.order-list-type:: number
	- Example:
	  ```yaml
	  addons:
	    config-locator: "1.+"
	  ```