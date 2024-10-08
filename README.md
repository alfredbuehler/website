# Kanboard's Official Website Repository

This website is a simple HTML static webpage to serve [Kanboard](https://kanboard.org/ "Visit website").

### How to add a new plugin to the list?

1. Update the [**`plugins.json`**](https://github.com/kanboard/website/blob/main/plugins.json) file

   - **This file is now sorted alphabetically**
     - Your plugin submission should be positioned in the file in alphabetical order **by plugin name**
   - This file is used in the Kanboard interface Plugins Directory
   - Template:

   ```
   "MyPlugin": {
       "author": "Plugin Developer Name",
       "compatible_version": ">=1.2.20",
       "description": "My plugin description",
       "download": "https://github.com/PluginDeveloperName/MyPlugin/releases/download/v1.0/MyPlugin-1.0.zip",
       "has_hooks": false,
       "has_overrides": false,
       "has_schema": false,
       "homepage": "https://github.com/PluginDeveloperName/MyPlugin",
       "is_type": "plugin",
       "last_updated": "2022-11-10",
       "license": "MIT",
       "readme": "https://github.com/PluginDeveloperName/MyPlugin/blob/master/README.md",
       "remote_install": true,
       "title": "MyPlugin",
       "version": "1.0.0"
   }

   ```

2. Send a [Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork "You must fork the main repository before you can create a Pull Request") of your changes
   - Once merged, this will automatically update the above file(s) with your changes

---

### JSON Properties in `plugins.json`

Here’s a completed list with all fields:

- `author`
  - The name of the plugin developer or organization that created the plugin.
- `compatible_version`
  - This indicates the Kanboard version with which your plugin is tested and compatible. It typically follows the format `>=1.2.20` for compatibility.
- `download`
  - **Do not use the GitHub archive URL** for the download link:
    - Once unzipped, the directory structure is not the same as the one mentioned above. GitHub usually appends the branch name to the folder. **As a result, Kanboard won't be able to load the plugin**.
  - Make your own archive or set the `remote_install` field to `false`.
  - If you release a new version of your plugin, always cross-check the version numbers of your archive filename and the URL.
- `remote_install`
  - Allows people to install the plugin from the Kanboard user interface.
- The **last property** should **NOT** have a comma at the end of the line (before the closing curly bracket).
- The **last plugin** in the list should **NOT** have a comma at the end of the section (after the closing curly bracket).
- `has_schema`
  - `true` or `false`
  - Specify whether your plugin includes any database changes. This field should be of _Boolean type_.
- `has_overrides`
  - `true` or `false`
  - Specify whether your plugin includes any template overrides. This field should be of _Boolean type_.
- `has_hooks`
  - `true` or `false`
  - Specify whether your plugin uses any hooks. This field should be of _Boolean type_.
- `is_type`
  - `plugin` or `action` or `theme` or `multi` or `connector`
  - Specify the type of your plugin:
    | Value | Type | Description |
    | ----- | ---- | ----------- |
    | `plugin` | Normal | _A plugin with no automatic actions_ |
    | `action` | Action | _A plugin for actions only_ |
    | `theme` | Normal | _A plugin for theming and styling of the interface_ |
    | `connector` | Normal | _A plugin connecting to third party services - may contain actions_ |
    | `multi` | Normal | _A plugin containing all or any combination of the above functions_ |
  - This field should be of _String type_.
- `last_updated`
  - Format: `YYYY-MM-DD` (e.g., `2022-11-15`)
  - Specify the date when your plugin was last updated for general release. This field should be of _ISO-8601 date type_.

---

### Folder Structure

```
MyPlugin-1.0.0.zip      <= Zip archive filename stating release version
└── MyPlugin            <= Plugin name
    ├── Assets          <= Javascript/CSS files
    │   └── cs
    │   └── js
    ├── Controller
    ├── LICENSE         <= Plugin license
    ├── Helper
    ├── Locale
    │   └── fr_FR
    │   └── en_US
    |   ├── ...
    ├── Model
    ├── Plugin.php      <= Plugin registration file
    ├── README.md
    ├── Schema          <= Database migrations
    ├── Template        <= Template files
    │   ├── ...
    ├── Test            <= Unit tests
    │   └── ...
```

#### Important Notes

- The archive will be extracted by Kanboard into the `plugins` folder as `plugins/MyPlugin`.
- Your plugin archive **must contains a folder with the plugin name** (no branch name or version numbers, just the plugin name)
