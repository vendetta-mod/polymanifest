# polymanifest
A unified manifest format for Discord client mods.

## Specification
The file name for a polymanifest should always be `manifest.json`, as opposed to a mod-specific name like `powercord_manifest.json` or `cumcord_manifest.json`.

## Fields

* `name` - string, the name of the plugin. Has no length limit, and is allowed to contain spaces.

* `description` - string, a short description of the plugin.

* `authors` - array of objects containing metadata about the plugin's authors.
    * name - string, the name of the author
    * id - string, the user's ID on Discord

    An example of an author object might look like this:
    ```json
    {
        "name": "Beef",
        "id": "257109471589957632"
    }
    ```
    <sup>This field may be updated down the line to support more author metadata, like contact links.</sup>

* `main` - the name of the plugin's main file, such as `plugin.js` or `index.js`. Mods are expected to read this, and fetch accordingly.

* `hash` - the SHA-256 hash of the plugin's bundle. Mods can use this for updating, and it is expected to be added at build time, rather than in the developer-accessible manifest.

### Vendor-specific fields
There are situations where a mod may wish to specify it's own data, for example a plugin icon.

This is achieved via a vendor-specific field - an extension to the spec, preferably named after the mod in question. Here is an example:

```json
"vendetta": {
    "icon": "ic_mail"
}
```

Data inside the mod's field does not follow a set structure - it is up to the developer.

## Concerns

### The concept of a vendor-specific field breaks the idea of a "unified" format!
This is true, but I could not come up with a better solution. The hope is that a mod can also use it's vendor-specific field to determine that a plugin is intended for it.