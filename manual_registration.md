# Manual Registration in Slicer
The goal of this protocol is to describe how manual registration was performed and how it is being executed in our case for alignment of CT, MRI, template, obiturator, and catheter information.

>Before We Begin: The Available Tools
>1. Data
>>All nodes -> data_name -> Edit properties -> Information
>2. Volumes
>3. Models
>>Display -> Visibility -> [Visbility, Opacity, View, Color]
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
