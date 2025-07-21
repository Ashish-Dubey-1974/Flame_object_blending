# 🌟 Realistic Object Blending with Shadows using Light Direction

This project demonstrates an automated pipeline for **realistic object compositing**—seamlessly integrating a foreground object onto a background image with **depth-aware shadows** and **light direction estimation**.

---

## 📸 Sample Output


A person is placed onto a background image with a realistic shadow and lighting adjustment that matches the scene.

---

## 🎯 Objective

Blend a person/object into a background image such that:

- ✅ The background is removed from the object.
- ✅ Light direction is estimated automatically.
- ✅ Shadows are generated realistically using depth and light info.
- ✅ Object lighting is adjusted to match the background.

---

## 🧰 Technologies Used

| Tool/Library       | Purpose                        |
|--------------------|--------------------------------|
| Python             | Core scripting language        |
| OpenCV             | Image processing               |
| NumPy              | Array computations             |
| Pillow (PIL)       | Image I/O                      |
| rembg              | Background removal             |
| PyTorch + Torchvision | Depth estimation via MiDaS |
| MiDaS              | Monocular depth prediction     |
| OS                 | File path handling             |

---

## 📁 Project Structure

.
├── input/
│ ├── obj.jpg # Input object image
│ ├── obj_mask.png # Generated binary mask
│ └── output.png # Transparent PNG after background removal
├── generate_mask.py # Removes BG and creates mask
├── generate_shadow_output.py# Final blending and shadow generation
├── location.py # Light direction estimation
├── bg.jpg # Background image
├── enhanced_shadow_result.jpg # Final output image
└── comparison.jpg # Side-by-side comparison of before/after

yaml
Copy
Edit

---

## 🚀 How It Works

### Step 1: Background Removal
**File:** `generate_mask.py`

- Uses `rembg` to remove background.
- Converts alpha channel to binary mask.
- Applies Gaussian blur for refinement.

```bash
python generate_mask.py
Step 2: Light Direction Estimation
File: location.py

Converts background to grayscale.

Applies Gaussian blur.

Detects brightest point and estimates light direction.

bash
Copy
Edit
python location.py
Step 3: Depth Estimation
Function: estimate_depth(img) (inside generate_shadow_output.py)

Loads MiDaS model from PyTorch Hub.

Generates a depth map to influence shadow realism.

Step 4: Shadow Creation
Function: create_realistic_shadow(...)

Translates object mask based on light direction.

Adds soft, elongated shadows using Gaussian blur.

Adds grounding ellipse under object.

Step 5: Lighting Adjustment
Function: adjust_object_lighting(...)

Applies directional lighting gradient based on light direction vector.

Adjusts object brightness to match the scene.

Step 6: Final Blending
Function: enhanced_blend_object_shadow(...)

Places the object into the background.

Blends object and shadows realistically.

Saves final composited image and comparison view.

bash
Copy
Edit
python generate_shadow_output.py
📦 Output
enhanced_shadow_result.jpg: Final composited image.

comparison.jpg: Side-by-side view of background vs composited output.

💡 Future Improvements
Better color tone matching between object and background.

Handle indoor/outdoor lighting scenarios differently.

Support for multiple light sources and shadows.

📄 License
This project is for educational and academic use only.
