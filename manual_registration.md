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
>>
>>To render multiple overlapping volumes: Display -> VTK Multi-Volume. Has limitations. The volume must not be under an affine transformation; warped volumes must have had their transforms hardened.

Finally, if the application crashes when rotating or zooming a volume, TDR error occurred indicating GPU overwhelmed by volume rendering. Either reduce the volume size, use CPU, increase TDR delay time, or update graphics card.


