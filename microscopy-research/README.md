# Edinburgh BA41/42 TEM: four-image test subset

This is a small extract from the verified 120-image package: two Alzheimer's and two control full-resolution TIFFs, with one image from each of four distinct de-identified donors. Each TIFF has its matching .metadata.json sidecar. The four-row manifest lists the donor identifier, original DM3 filename, original source, pixel verification status and checksums.

Source and attribution: Spires-Jones, Tara (2018), *Region-specific depletion of synaptic mitochondria in the brains of patients with Alzheimer's disease - TEM data*, University of Edinburgh DataShare, https://doi.org/10.7488/ds/2417. Associated paper: Pickett et al. (2018), https://doi.org/10.1007/s00401-018-1903-2. License: Creative Commons Attribution 4.0 International, https://creativecommons.org/licenses/by/4.0/ . Attribute the source when sharing.

The source DM3 pixel arrays were copied to TIFF without contrast adjustment, resizing, normalization or other image processing. TIFF data types, dimensions and pixel bytes were verified against the originals during conversion. Each sidecar retains DM3 metadata, pixel calibration and microscope magnification. This convenience sample does not represent an independent donor-level study; use donor-level splits for any model evaluation.


## Repository layout

| Path | Contents |
| --- | --- |
| `Alzheimers/`, `Control/` | Full-resolution float32 TIFFs, byte-identical to the source ZIP. |
| `previews/Alzheimers/`, `previews/Control/` | 16-bit grayscale PNG previews, one per TIFF. |
| `metadata/` | The `.tif.metadata.json` sidecar for each TIFF, unchanged. |
| `manifest.csv` | One row per image. |

The ZIP itself is not in this repository.

## Manifest

`manifest.csv` keeps every column of the source manifest, including donor identifier, coded case, original DM3 filename and checksums. `experimental_group` holds the group label. `image_metadata_sidecar` now points into `metadata/`. Six columns are new: `tiff_path`, `png_preview_path`, `png_preview_bit_depth`, `png_scale_min`, `png_scale_max` and `png_preview_sha256`. All paths are relative to this folder. File names contain spaces, so URL-encode them as `%20` in links.

## PNG previews

The TIFFs store float32 values, and PNG cannot. Each preview is a full-resolution, 16-bit grayscale PNG. The image's own minimum and maximum map linearly to 0 and 65535, with no clipping, resizing or filtering. To recover the original values:

`value = png_scale_min + pixel / 65535 * (png_scale_max - png_scale_min)`

On these four images the recovered values differ from the TIFF by at most 0.68 intensity units, half a quantization step. A few outlier pixels set each image's range, so previews look flat, and brightness does not compare across previews. Use the TIFFs for any quantitative work.

CC BY 4.0 requires a note on changes. The PNG previews are adaptations of the TIFFs made by the rescaling above. The TIFFs and sidecars are unmodified copies of the source files. Attribution and license in the first section apply to every file in this folder.
