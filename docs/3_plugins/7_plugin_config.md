
# Plugin Config

## Configuration

To register and display custom plugins in RBrowser, export a `pluginConf` array where each entry defines a plugin’s behavior and placement. Each plugin object supports the following properties:

- **`id`**  
  A unique string identifier for the plugin.

- **`name`**  
  The human-readable label shown in the UI.

- **`element`**  
  The React component to render (TSX element).

- **`position`**  
  Where to dock the plugin panel (`left`, `middle`, `right`).

- **`order`**  
  Numerical order among sibling plugins (lower numbers render first).

- **`setting`** _(optional)_  
  An object of initial settings, e.g. `{ visible: true }` to show by default.

### Example (TypeScript)

```Typescript

import TranscriptBrowser from '@/views/main/c-views/transcript'
import RNA2DStructure from '@/views/main/c-views/rna_2d_structure'

export const pluginConf = [
  {
    id: 'transcript browser',
    name: 'Transcript Browser',
    element: <TranscriptBrowser />,
    position: 'middle',
    order: 1,
    setting: {
      visible: true
    }
  },
  {
    id: 'rna-2d-structure',
    name: '2D RNA Structure',
    element: <RNA2DStructure />,
    position: 'right',
    order: 1
  }
]

```