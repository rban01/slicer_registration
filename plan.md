# 🧭 Hardware-First CT→MRI Manual Registration Checklist (3D Slicer)

## 1. Load Data
- [ ] Load **MRI** and **CT** in **Data** module.  
- [ ] Set **MRI → Fixed**, **CT → Moving**.  
- [ ] Load **applicator models** (template, obturator, etc.).  

---

## 2. Create Transform
- [ ] In **Transforms**, create **Linear Transform** → rename → `CT_to_MRI_transform`.  
- [ ] In **Data**, parent **CT volume** + **models** under this transform.  
  > ✅ Moves CT + hardware as one rigid block.

---

## 3. Visualization Setup
- [ ] **Volumes module** → Adjust **CT window/level** for metal/bone.  
- [ ] Adjust **MRI display** for soft-tissue contrast.  
- [ ] Turn on **Red/Yellow/Green** slice views and **link slices**.  
- [ ] Use **CT opacity 50–70 %** (volume blending).  
- [ ] Enable **Slice intersections** (`Ctrl + Shift + I`).  

---

## 4. Coarse Alignment
- [ ] Select **CT_to_MRI_transform**.  
- [ ] In 3D or slice views, use **translation/rotation handles**.  
- [ ] Align **template plane orientation** (e.g., axial plane alignment).  

---

## 5. Fine Alignment (Hardware-First)
- [ ] Zoom in on:
  - **Obturator tip**  
  - **Template grooves / flange borders / metal sleeves**  
- [ ] Match these CT-bright features to their faint MRI counterparts.  
- [ ] Keep CT + hardware rigid; adjust transform only.  

---

## 6. Continuous Cross-Checks
- [ ] **Red slice:** Check obturator tip depth.  
- [ ] **Yellow/Green slices:** Check lateral slot positions & curvature.  
- [ ] **3D view:** Confirm obturator axis passes through template center.  
- [ ] **Shift + Mouse drag** in slice → scrub along catheter paths for sanity check.  

---

## 7. Validation & Finalization
- [ ] When satisfied → **Right-click → Harden Transform** (CT + models).  
- [ ] Optionally remove transform node.  
- [ ] (Optional) Use **Segment Editor → Paint** to mark anatomical landmarks for overlay check.  
- [ ] (Optional) Refine using:
  - **Landmark Registration** (paired fiducials)  
  - **Surface Registration (ICP)**  

---

## 8. Optional 3D Review
- [ ] Enable **Volume Rendering**:
  - **CT:** bone/metal threshold.  
  - **MRI:** soft-tissue view.  
- [ ] Verify **voxel spacing** in *Volumes → Volume Information*.  

---

## ⚙️ Core Principle
> **Rigid hardware defines the reference frame.**  
> Align CT’s bright applicator geometry to its faint but spatially consistent MRI counterpart.  
> Anatomy follows the hardware alignment.
