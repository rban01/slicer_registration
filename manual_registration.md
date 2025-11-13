# Manual Registration in Slicer
The goal of this protocol is to describe how manual registration was performed and how it is being executed in our case for alignment of CT, MRI, template, obiturator, and catheter information.

>Before We Begin: The Available Tools
>1. Data
>>All nodes -> data_name -> Edit properties -> Information
>2. Volumes
>>Volume node stores voxels (3D arrays).
>>
>>Grid axes can be positioned and oriented in physical space.
>>
>>Axes may have different spacing.
>>
>>CT and MRI images are scalar volumes.
>>
>>Volumes handle 2D images as a single-slice 3D image.
>>
>>Overlay Volumes: Load both -> Data module -> Left click on background volume, then right clikc on foreground volume and set it to foreground
>>
>>Use link to make changes apply to all volumes in view group.
>>
>>Image spacing: Distance [mm] between pixel centers when mapped to patient space
>>
>>Image Origin: Center of (0,0,0) IJK pixel expressed wrt patient space. Patient space organized wrt to subject Right, Anterior, and Superior anatomical directions.
>>
>>To render different volumes in two views, go to Dual 3D and drag and drop each volume into the 3D view from the Data module.
>3. Models
>>Display -> Visibility -> [Visbility, Opacity, View, Color]
>>
>>View specifies in which view the model is visible. If none are checked, the model is visible in all views, 2D or 3D.
>4. Transforms
>5. Markups
>6. Segment Editor
>7. Four-Up
>8. Translate/rotate view, adjust displayed objects
>9. Adjust window/level of volume by left-click-and-drag slice views
>10. Toggle Markups Toolbar
>11. Toggle Crosshair Visibility
>12. Toggle Slice Intersection Visibility

In our case, we have an obiturator, a vtkPolyData Model surface mesh imported as a .stl file, and likewise for the template.<br><br>
CT and MRI data contain two volumes.<br><br>
We need to align obiturator and template to projection in MRI, align CT with MRI, and then bring in the catheters and match them up as well.

>How to Hide Certain Regions of a Volume
>
>If a portion cannot be hidden using the cropping box/ROI, then:
>
>Segment Editor -> Paint/Scissors to specify region -> Mask volume effect to fill region with empty values -> Hide volume rendering of original volume and set up rendering for masked vol -> Update using Masked volume effect

>Panels and their use (volume rendering)
>>Inputs: List of nodes for VolumeRendering.
>>
>>Volume: Select volume to render (one at a time)
>>
>>Display: Select current volume rendering display properties. Display nodes have inof related to the rendering (pointers to ROI, volume proprty, view nodes). New display node is automatically created if none exist for current volume.
>>
>>ROI: Select current ROI
>>
>>View: As above.


Limitations
To render multiple overlapping volumes, select “VTK Multi-Volume” rendering in “Display” section. This renderer is still experimental and has limitations such as:

Cropping is not supported (cropping ROI is ignored)

RGB volume rendering is not supported (volume does not appear)

Only “Composite with shading” rendering technique is supported (volume does not appear if “Maximum Intensity Projection” or “Minimum Intensity Projection” technique is selected)

To reduce staircase artifacts during rendering, choose enable “Surface smoothing” in Advanced/Techniques/Advanced rendering properties section, or choose “Normal” or “Maximum” as quality.

The volume must not be under a warping (affine or non-linear) transformation. To render a warped volume, the transform must be hardened on the volume. (see related issue)

If the application crashes when rotating or zooming a volume: This indicates that you get a TDR error, i.e., the operating system shuts down applications that keep the graphics card busy for too long. This happens because the size of the volume is too large for your GPU to comfortably handle. There are several ways to work around this:

Option A: Run the code snippet in the Python console (Ctrl-3) to split the volume to smaller chunks (that way you have a better chance that the graphics card will not be unresponsive for too long).

slicer.vtkMRMLVolumeRenderingDisplayableManager.SetMaximum3DTextureSize(400)
for vrDisplayNode in getNodesByClass('vtkMRMLVolumeRenderingDisplayNode'):
    slicer.util.arrayFromVolumeModified(vrDisplayNode.GetVolumeNode())
Option B: Crop and downsample your volume using Crop volume and volume render this smaller volume.

Option C: Increase TDR delay value in registry (see details here)

Option D: Use CPU volume rendering.

Option E: Upgrade your computer with a stronger graphics card.
