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

## Concerns

### How can a mod determine that a plugin is intended to be used with it?
A solution for this would be to extend the spec with a field for the mod, however I feel this defeats the point of a "unified manifest format".