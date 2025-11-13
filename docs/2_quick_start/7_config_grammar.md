# RBrowser Renderer

## Configuration

### `renderer`  

  Type: [IRenderer](#irenderer)

  Global rendering settings:  

  - **`containerId`** (string)  
    ID of the DOM element into which the canvas is mounted (e.g., `"tb-rna"`).  
  - **`backgroundColor`** (string)  
    Canvas background color (e.g., `"#ffffff"`).  
  - **`resolution`** (`"auto"` | number)  
    Pixel ratio; `"auto"` matches the device DPR, or set a fixed value.

---

### `target`  

Type: [ITarget](#itarget)

Defines which gene and transcript to display:  

- **`dna`** (string)  
  DNA-level identifier (e.g., `"vamp3"`).  
- **`rna`** (string)  
  Transcript-level identifier (e.g., `"vamp3-201"`).

---

### `region`  

Type: [IRegion](#iregion)

Specifies the genomic window to visualize:  

- **`chr`** (string)  
  Chromosome name (e.g., `"chr11"`).  
- **`start`** (number)  
  0-based start coordinate (e.g., `66316918`).  
- **`end`** (number)  
  End coordinate (e.g., `66318628`).  
- **`offset`** (number)  
  Upstream/downstream padding in base pairs (e.g., `10000`).

---

### `channels`  

Type: [IChannel](#ichannel)

An array of track definitions; each object configures one visual channel:  

- **`name`** (string)  
  Display label for the track.  
- **`plot`** (string)  
  Visualization type (e.g., `"sequence"`, `"transcript"`, `"rect"`, `"point"`, `"bar"`, `"angle"`, `"snm"`).  
- **`level`** (optional, `"dna"` | `"rna"`)  
  Coordinate space for rendering; defaults to `"rna"`.  
- **`style`** (optional, object)  
  Custom appearance settings, e.g. `{ height: 100 }` or `{ color: "#70a1ff" }`.  
- **`data`** (object)  
  Data source configuration:  
  - **`method`** (`"built-in"` | `"remote"`)  
  - **`format`** (string)  
    Data format (e.g., `"fasta"`, `"gff"`, `"bigwig"`, `"bed"`, `"bigbed"`, `"exon_expression"`, `"junction_expression"`, `"modification"`, `"ccre"`, `"rbp"`, `"eqtl"`, `"sqtl"`).  
  - **`url`** (string)  
    Endpoint or local key for loading data.  
  - **`index`** (string, optional)  
    URL to an index file (e.g., `.tbi`, `.bbx`).  
  - **`type`** (string, optional)  
    Subtype for modifications (e.g., `"m6a"`, `"Ψ"`).

---

### **Default Values**  

- `renderer.resolution`: `"auto"`  
- `region.offset`: `0`  
- Any channel without explicit `style` or `level` will use framework defaults.  

## Interfaces

This document describes the core TypeScript interfaces used to configure the RBrowser renderer, region selection, channels, and overall track configuration.

---

### `IRenderer`  
Global rendering settings for the canvas and application instance.

| Property            | Type                                   | Description                                                                                 |
| ------------------- | -------------------------------------- | ------------------------------------------------------------------------------------------- |
| `containerId`       | `string`                               | ID of the DOM element into which the PIXI canvas is mounted.                                 |
| `type?`             | `string`                               | Optional renderer type identifier (e.g. `"webgl"`, `"canvas"`).                             |
| `resolution?`       | `number` \| `"auto"`                   | Pixel ratio: `"auto"` matches device DPR; or set a fixed numeric value.                     |
| `backgroundColor?`  | `number` \| `string`                   | Canvas background color (hex string or numeric color code).                                 |
| `isDebug?`          | `boolean`                              | Enable debug mode (renders diagnostic overlays, logs).                                      |
| `colors?`           | `string[]`                             | Array of color strings used for default track color palettes.                               |
| `app?`              | `PIXI.Application<HTMLCanvasElement>`  | Optional existing PIXI Application instance to reuse.                                       |
| `layout?`           | `ILayout`                              | Default layout margins and paddings for renderer chrome (see below).                        |

---

### `ITarget`  
Identifiers for different molecular targets.

| Property  | Type     | Description                              |
| --------- | -------- | ---------------------------------------- |
| `dna?`    | `string` | DNA-level identifier (e.g. gene name).   |
| `rna?`    | `string` | Transcript-level identifier.             |
| `protein?`| `string` | Protein-level identifier.                |

---

### `ILayout`  
Margin, padding, and element sizing used by renderer and channels.

| Property         | Type     | Description                                     |
| ---------------- | -------- | ----------------------------------------------- |
| `marginTop?`     | `number` | Top margin in pixels.                           |
| `marginLeft?`    | `number` | Left margin in pixels.                          |
| `marginBottom?`  | `number` | Bottom margin in pixels.                        |
| `paddingTop?`    | `number` | Top padding in pixels.                          |
| `paddingBottom?` | `number` | Bottom padding in pixels.                       |
| `lineHeight?`    | `number` | Default line height for text labels.            |
| `eleWidth?`      | `number` | Default width for rendered elements.            |

---

### `IRegion`  
Defines a genomic or transcriptomic interval to display.

| Property     | Type                 | Description                                                                 |
| ------------ | -------------------- | --------------------------------------------------------------------------- |
| `index?`     | `string`             | Optional unique identifier for the region.                                  |
| `chr`        | `string`             | Chromosome name (e.g. `"chr11"`).                                           |
| `start`      | `number`             | 0-based start coordinate.                                                   |
| `end`        | `number`             | End coordinate (exclusive).                                                 |
| `status?`    | `RegionStatus`       | Optional status enum (e.g. `"loading"`, `"ready"`, `"error"`).              |

---

### `IChannel`  
Configuration for a single visual track (“channel”) in the browser.

| Property             | Type                                        | Description                                                                                           |
| -------------------- | ------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `name?`              | `string`                                    | Display label of the channel (e.g. `"M6A-Modifications"`).                                             |
| `sort?`              | `number`                                    | Optional sort index for ordering channels.                                                             |
| `index?`             | `string`                                    | Unique channel identifier.                                                                             |
| `level?`             | `string`                                    | Coordinate space (`"dna"`, `"rna"`, etc.).                                                            |
| `target?`            | `string`                                    | Optional data target key (e.g. transcript ID).                                                         |
| `app?`               | `PIXI.Application`                          | Optional PIXI instance for this channel.                                                               |
| `data?`              | `any`                                       | Raw data payload or fetch configuration.                                                               |
| `record?`            | `any`                                       | Parsed record cache for faster redraws.                                                                |
| `textures?`          | `any`                                       | PIXI textures or sprite sheets used by this channel.                                                   |
| `error?`             | `string`                                    | Error message if data loading or rendering fails.                                                      |
| `removable?`         | `boolean`                                   | Whether the user can remove this channel.                                                              |
| `isRemoved?`         | `boolean`                                   | Internal flag indicating removal state.                                                                |
| `draggable?`         | `boolean`                                   | Enables drag-and-drop reordering of this channel.                                                      |
| `gindex?`            | `string`                                    | Group index for batch operations across related channels.                                              |
| `maxRows?`           | `number`                                    | Maximum number of rows (for multi-row plots).                                                          |
| `order?`             | `number`                                    | Rendering order relative to sibling channels.                                                          |
| `plot?`              | `IRenderPlot`                               | Plotting style configuration (points, bars, lines, etc.).                                             |
| `normalization?`     | `"min"` \| `"max"` \| `"mean"` \| `"none"`  | Data normalization method.                                                                             |
| `scale?`             | `"log"` \| `"none"`                         | Scale transformation for quantitative tracks.                                                          |
| `style?`             | `IStyle`                                    | Custom visual styling (colors, heights, shapes).                                                       |
| `layout?`            | `ILayout`                                   | Channel-specific layout overrides.                                                                     |
| `region?`            | `IRegion` \| `IRegion[]`                    | One or more regions displayed in this channel.                                                         |
| `view?`              | `IView`                                     | Optional view context (e.g. zoom, pan state).                                                          |
| `group?`             | `string`                                    | Logical grouping key (e.g. tissue type, assay).                                                        |
| `slice?`             | `Slice`                                     | Subsetting or windowing instructions for large datasets.                                               |
| `renderDirection?`   | `"left"` \| `"right"`                       | Direction in which to draw oriented elements (e.g. transcripts).                                       |

---

### `ITRConfig`  
Top-level configuration object that ties together the renderer, region, channels, axis, and targets.

| Property    | Type                         | Description                                                                 |
| ----------- | ---------------------------- | --------------------------------------------------------------------------- |
| `renderer`  | `IRenderer`                  | Canvas and renderer settings (see above).                                   |
| `region`    | `IRegion`                    | Primary display region.                                                     |
| `channels`  | `IChannel[]`                 | Array of channel configurations.                                            |
| `axis?`     | `IAxis`                      | Optional axis styling and tick settings (color, fontSize, interval, etc.). |
| `target?`   | `{ dna?: string; rna?: string; protein?: string }`  | Optional identifiers for DNA, RNA, and protein targets.     |

## Example (TypeScript)

```TypeScript
export const rendererRNAConfig: IRNAConfig = {
  renderer: {
    containerId: 'tb-rna',
    backgroundColor: '#ffffff',
    resolution: 'auto'
  },
  target: {
    dna: 'vamp3',
    rna: 'vamp3-201'
  },
  region: {
    chr: 'chr11',
    start: 66316918,
    end: 66318628,
    offset: 10000
  },
  channels: [
      {
      name: "CCRE",                 // Track display name
      plot: "rect",                 // Rendering type: rectangular annotations

      group: {
        name: "DNA Annotation",     // Track group/category label
        style: {
          color: "#54a24b"          // Accent color for group header/legend
        }
      },

      data: {
        method: "remote",           // Data source is remote (fetched over HTTP)
        format: "bigbed",           // File format of the data
        url: "https://data.rbrowser.org/datahub/ccre/all_sim_ccre.bigBed" // BigBed endpoint
      },

      annotation: {
        // Column keys extracted from the BigBed "name" (or extra) field after splitting
        // The order must match the order in the encoded string.
        keys: ["Element", "Element ID", "ENCODE ID", "Feature"],

        // When set, the viewer expands items by the given key (e.g., split a combined track
        // into sub-tracks per Element). NOTE: enabling `expand` disables lazy loading.
        expand: "Element",

        // Color mapping used when `expand` is active.
        // Each Element value is assigned a specific color in the legend and glyphs.
        // If a value is not present in this map, a default color will be used.
        colors: {
          CTCF: "purple",
          "Distal Enhancer like": "brown",
          "Proximal Enhancer like": "yellow",
          "Promoter like": "green",
          "Chromatin Accessible": "sky"
        },

        // Separator used to split the annotation field into the `keys` above.
        sep: "|"
      },

      // Optional filter expression (empty string = no filtering).
      // Example: "Element=Promoter like" or "Feature~enhancer"
      filter: ""
    },
    {
      name: 'Fasta',
      plot: 'sequence',
      level: 'rna',
      data: {
        method: 'built-in',
        format: 'fasta',
        url: 'fasta'
      }
    },
    {
      name: 'Single molecule modifications',
      plot: 'transcript',
      style: {
        height: 100
      },
      data: {
        method: 'remote',
        format: 'gff',
        url: 'https://data.rbrowser.org/channels/gencode.v44.basic.sorted.gff.gz',
        index: 'https://data.rbrowser.org/channels/gencode.v44.basic.sorted.gff.gz.tbi'
      }
    },
    {
      name: 'RNA',
      plot: 'rect',
      level: 'rna',
      data: {
        method: 'built-in',
        format: 'rna',
        url: 'rna'
      }
    },
    {
      name: 'All Exon',
      level: 'rna',
      plot: 'rect',
      data: {
        method: 'built-in',
        format: 'exon_expression',
        url: 'exon_expression'
      }
    },
    {
      name: 'Junction',
      level: 'rna',
      plot: 'angle',
      data: {
        method: 'built-in',
        format: 'junction_expression',
        url: 'junction_expression'
      }
    },
    {
      name: 'M6A-Modifications',
      level: 'rna',
      plot: 'point',
      data: {
        method: 'built-in',
        format: 'modification',
        url: 'modification',
        type: 'm6a'
      }
    },
    {
      name: 'Ψ-Modifications',
      level: 'rna',
      plot: 'point',
      data: {
        method: 'built-in',
        format: 'modification',
        url: 'modification',
        type: 'Ψ'
      }
    },
    {
      name: 'CCRE',
      level: 'rna',
      plot: 'rect',
      data: {
        method: 'built-in',
        format: 'ccre',
        url: 'ccre'
      }
    },
    {
      name: 'RBP',
      level: 'rna',
      plot: 'rect',
      data: {
        method: 'built-in',
        format: 'rbp',
        url: 'rbp'
      }
    },
    {
      name: 'eQTLs',
      level: 'rna',
      plot: 'point',
      data: {
        method: 'built-in',
        format: 'eqtl',
        url: 'eqtl'
      }
    },
    {
      name: 'sQTLs',
      level: 'rna',
      plot: 'point',
      data: {
        method: 'built-in',
        format: 'sqtl',
        url: 'sqtl'
      }
    },
    {
      name: 'caRNA (GM18499)',
      plot: 'bar',
      style: {
        color: '#70a1ff'
      },
      data: {
        method: 'remote',
        format: 'bigwig',
        url: 'https://data.rbrowser.org/datahub/merip/caRNA_MeRIP-seq/Input/1..GM18499..caRNA_MeRIP_Input.bw'
      }
    },
    {
      name: 'caRNA (GM19099)',
      plot: 'bar',
      style: {
        color: '#70a1ff'
      },
      data: {
        method: 'remote',
        format: 'bigwig',
        url: 'https://data.rbrowser.org/datahub/merip/caRNA_MeRIP-seq/Input/10..GM19099..caRNA_MeRIP_Input.bw'
      }
    },
    {
      name: 'BEDrm support',
      plot: 'snm',
      style: {
        height: 100
      },
      data: {
        method: 'remote',
        format: 'bed',
        url: 'https://data.rbrowser.org/channels/nanopore_m6a.bed.gz',
        index: 'https://data.rbrowser.org/channels/nanopore_m6a.bed.gz.tbi'
      }
    },
    {
      name: 'CTCF (ChIP-seq)',
      plot: 'rect',
      data: {
        method: 'remote',
        format: 'bigbed',
        url: 'https://www.encodeproject.org/files/ENCFF522RNT/@@download/ENCFF522RNT.bigBed'
      }
    }
```