# cfd-yplus-mesh-calculator

<div align="center">

![CFD y⁺ Calculator](https://img.shields.io/badge/CFD-y%E2%81%BA%20%26%20Mesh%20Calculator-00d4ff?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0tMSAxNEg5VjhoMnY4em00IDBoLTJWOGgydjh6Ii8+PC9zdmc+)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![No Dependencies](https://img.shields.io/badge/Dependencies-None-00ff9d?style=for-the-badge)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

**An interactive, beginner-friendly CFD pre-processing tool that translates flow physics into practical near-wall mesh parameters — bridging theory and real-world meshing decisions.**

[🚀 Live Demo](#) · [📖 Documentation](#how-it-works) · [🐛 Report Bug](../../issues) · [✨ Request Feature](../../issues)

</div>

---

## 📸 Preview

> A dark-themed, engineering-grade single-page web app with animated visuals, real-time calculations, and intelligent turbulence model guidance.

---

## 🔬 What Is This?

The **CFD y⁺ & Mesh Calculator** is a zero-dependency, single-file HTML tool designed for CFD practitioners and students who need to quickly determine near-wall mesh parameters before meshing in **ANSYS Fluent**, **OpenFOAM**, or **STAR-CCM+**.

Instead of manually working through skin-friction correlations and unit conversions, you simply enter your flow conditions and desired y⁺, and the tool instantly returns everything you need to configure your inflation layers.

---

## ✨ Features

- **Reynolds Number** with automatic flow regime classification (Laminar / Transitional / Turbulent)
- **Skin Friction Coefficient** — Prandtl correlation for external flow, Blasius for internal flow
- **Wall Shear Stress** and **Friction Velocity** calculations
- **First Cell Height (Δy₁)** output in both metres and millimetres — the key meshing parameter
- **Boundary Layer Thickness (δ)** with recommended growth rate and layer count
- **Turbulence Model Recommendation** with detailed justification (k-ω SST, k-ε, LES)
- **Intelligent Warnings** — compressibility, laminar regime detection, oversized first cell, y⁺ extremes
- **y⁺ Quick Presets** — one-click buttons for y⁺ = 1, 5, 30, 100
- **Near-Wall SVG Schematic** — annotated diagram of Δy₁ and δ
- **Engineering Assumptions Panel** — expandable accordion explaining validity range
- **Typical Applications** reference section
- **Input Validation** — prevents zero/negative/missing values
- **No libraries, no frameworks, no build step** — pure HTML/CSS/JS, open in any browser

---

## ⚙️ Physics & Equations

All calculations are based on well-established empirical turbulent flow correlations.

### Reynolds Number
```
Re = ρ · U · L / μ          (external flow, L = characteristic length)
Re = ρ · U · D / μ          (internal flow, D = hydraulic diameter)
```

### Skin Friction Coefficient
```
Cf = 0.026 · Re^(-1/7)      (Prandtl, external turbulent flat plate)
Cf = 0.079 · Re^(-0.25)     (Blasius, internal turbulent pipe)
```

### Wall Shear Stress
```
τ_w = 0.5 · ρ · U² · Cf
```

### Friction Velocity
```
u_τ = √(τ_w / ρ)
```

### First Cell Height (Wall Spacing)
```
Δy₁ = y⁺ · μ / (ρ · u_τ)
```

### Boundary Layer Thickness (Prandtl 1/7-power law)
```
δ = 0.37 · L · Re^(-1/5)
```

---

## 🧮 Turbulence Model Guidance

| y⁺ Range | Recommended Model | Notes |
|----------|-------------------|-------|
| y⁺ ≈ 1 | k-ω SST / LES | Resolves viscous sublayer; no wall functions needed |
| y⁺ ≈ 2–10 | k-ω SST (Enhanced Wall Treatment) | Buffer layer; use enhanced wall treatment in Fluent |
| y⁺ ≈ 30–300 | k-ε Realizable / Standard | Log-law region; standard wall functions applicable |
| y⁺ > 300 | k-ε with Scalable Wall Functions | Accuracy degrades; refine critical regions if possible |

---

## ⚠️ Engineering Assumptions

This tool uses empirical correlations valid under the following conditions:

- Fully turbulent, wall-bounded flow
- Hydraulically smooth wall (no surface roughness)
- Zero pressure gradient (flat-plate / fully-developed approximation)
- Incompressible flow: **Mach < 0.3** (a warning is shown if exceeded)
- Uniform free-stream conditions

> Results are for **preliminary estimation only**. Always validate with a mesh independence study.

---

## 🚀 Getting Started

### Option 1 — Open Directly (Recommended)

```bash
# Clone the repository
git clone https://github.com/YOUR-USERNAME/cfd-yplus-mesh-calculator.git

# Open in browser — no server needed
open cfd_yplus_calculator.html        # macOS
start cfd_yplus_calculator.html       # Windows
xdg-open cfd_yplus_calculator.html   # Linux
```

### Option 2 — GitHub Pages

1. Fork this repository
2. Go to **Settings → Pages**
3. Set source to `main` branch, `/ (root)`
4. Your calculator will be live at `https://YOUR-USERNAME.github.io/cfd-yplus-mesh-calculator/`

### Option 3 — Direct Download

Download `cfd_yplus_calculator.html` and open it in any modern browser. No installation required.

---

## 📁 Repository Structure

```
cfd-yplus-mesh-calculator/
│
├── cfd_yplus_calculator.html   # Complete single-file application
├── README.md                   # This file
└── LICENSE                     # MIT License
```

---

## 🧪 Example Usage

**Scenario:** Turbulent airflow over a flat plate at 30 m/s

| Input | Value |
|-------|-------|
| Velocity U | 30 m/s |
| Density ρ | 1.225 kg/m³ |
| Dynamic Viscosity μ | 1.8 × 10⁻⁵ Pa·s |
| Flow Type | External |
| Characteristic Length L | 1.0 m |
| Desired y⁺ | 1 |

**Expected outputs (approximate):**

| Output | Value |
|--------|-------|
| Reynolds Number | ~2.04 × 10⁶ |
| Skin Friction Coefficient | ~3.5 × 10⁻³ |
| Wall Shear Stress | ~1.92 Pa |
| Friction Velocity | ~1.25 m/s |
| First Cell Height Δy₁ | ~0.00117 mm |
| Boundary Layer Thickness δ | ~19.3 mm |
| Recommended Model | k-ω SST / LES |

---

## 🎯 Typical Applications

- **External Aerodynamics** — Wings, airfoils, vehicle bodies, fuselages
- **Internal Pipe & Duct Flow** — HVAC, hydraulic systems, water treatment
- **Heat Transfer Simulations** — Conjugate heat transfer, cooling channels
- **Combustion Chamber Walls** — Gas turbines, IC engines

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "Add: description of change"`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

### Ideas for contribution

- [ ] Roughness effects (equivalent sand roughness k_s)
- [ ] Compressible flow correction (Mach > 0.3)
- [ ] Export results as PDF / CSV
- [ ] Additional fluids presets (water, oil, natural gas)
- [ ] Growth ratio optimizer given total BL thickness and layer count
- [ ] Transition prediction (Michel criterion)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- Empirical correlations from **Schlichting, H. — Boundary Layer Theory** (McGraw-Hill)
- Skin friction formulas: **Prandtl** (external) and **Blasius** (internal)
- Boundary layer model: **Prandtl's 1/7 power law**

---

<div align="center">

*This tool translates CFD flow physics into practical near-wall mesh parameters, bridging theory and real-world meshing decisions.*

**Built for students, researchers & entry-level engineers working with ANSYS Fluent and OpenFOAM.**

⭐ If this tool helped you, consider giving the repository a star!

</div>

