# Region

## Search Region

Users can enter a region of interest in the **Search Input** at the top navigation bar and click the search button to navigate to that interval.  

- Supports switching the rendered interval by **genomic coordinates**  
- Supports rendering by **RNA coordinates + flanking regions**  
- Supports rendering by **Gene ID + flanking regions**  

![Search Region](../imgs/2_quick_start/quick_start_navi_search.gif)

## Highlight Region

- **Single selection**  

    Hold the <kbd>Mouse Right</kbd> and drag over a region of interest to highlight it.  
    The highlight icon in the top-right corner toggles the visibility of the current highlighted region.

    ![Single Highlight](../imgs/2_quick_start/quick_start_navi_highlight.gif)

- **Multiple selection**  

    Hold <kbd>Ctrl</kbd> + <kbd>Mouse Right</kbd> drag to select and highlight multiple regions at once. 

    ![Multiple Highlights](../imgs/2_quick_start/quick_start_regions-0.png)

## Region Management

After selecting one or more regions, you can edit them in the **Region Panel** on the left sidebar.

### Switching Region Modes

- **DNA Mode**  

    Regions are displayed using traditional genomic (chromosome) coordinates.  

    ![DNA Mode Regions](../imgs/2_quick_start/quick_start_regions-1.png)

- **RNA Mode**  

    Regions record and display only intervals **within** the spliced transcript.  
    
    ![RNA Mode Regions](../imgs/2_quick_start/quick_start_regions-3.png)

- **CDS Mode**  
    Regions span only the **coding sequence**, skipping introns and UTRs.

### Adding a Region

Click the **＋** button in the panel’s top-right corner to add a new highlighted region.

### Editing a Region

Click the **start** or **end** coordinate under **Location** to modify the selected region.

### Removing a Region

Click the **trash** (delete) icon to remove the corresponding region.
