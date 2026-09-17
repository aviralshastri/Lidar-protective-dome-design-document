# Protective Transparent Enclosure for LightWare SF45/B LiDAR

> Engineering study and design brief for developing a transparent protective housing for a LightWare SF45/B scanning LiDAR while minimizing optical and environmental performance degradation.

---

## Table of Contents

- [Overview](#overview)
- [The Sensor](#the-sensor)
- [Problem Statement](#problem-statement)
- [Design Requirements](#design-requirements)
- [Proposed Enclosure Concept](#proposed-enclosure-concept)
- [Optical Phenomena](#optical-phenomena)
- [Environmental Effects](#environmental-effects)
- [Mechanical and Thermal Effects](#mechanical-and-thermal-effects)
- [Optical Material Requirements](#optical-material-requirements)
- [Candidate Materials](#candidate-materials)
- [Flat Window vs Curved Dome](#flat-window-vs-curved-dome)
- [Calibration Strategy](#calibration-strategy)
- [Experimental Validation Plan](#experimental-validation-plan)
- [Acceptance Criteria](#acceptance-criteria)
- [Questions for Optical/LLM Analysis](#questions-for-opticalllm-analysis)
- [Expected Deliverables](#expected-deliverables)
- [Important Engineering Principle](#important-engineering-principle)
- [References](#references)

---

## Overview

This repository documents the investigation and design of a **transparent protective enclosure for a LightWare SF45/B LiDAR**.

The primary goal is to protect the LiDAR from:

- Accidental manual contact
- Mechanical impact
- Dust
- Water and rain
- Dirt and contamination
- Outdoor environmental exposure
- Minor debris and foreign objects

The desired enclosure is a **continuous transparent cylindrical/domed housing** around the LiDAR.

The central engineering challenge is that the enclosure is not optically invisible. The 905 nm laser beam must pass through the protective material on its way to and from the target, meaning the enclosure becomes part of the optical system.

The design therefore needs to balance:

> **Mechanical protection + environmental protection + optical performance + manufacturability**

---

## The Sensor

The sensor under consideration is the **LightWare SF45/B (50 m)**.

According to LightWare's product information:

| Parameter | Specification |
|---|---|
| Sensor type | Single-beam oscillating LiDAR |
| Maximum horizontal scan | Up to 320° |
| Laser wavelength | 905 nm |
| Range | 0.2–50 m |
| Maximum readings | Up to 5,000 readings/s |
| Sweep rate | Up to 5 sweeps/s |
| Approx. dimensions | 51 × 48 × 44 mm |
| Approx. mass | 59 g |

**Important:** The SF45/B is officially specified as a **320° oscillating LiDAR**, not a 360° LiDAR.

Official product page:

https://lightwarelidar.com/shop/sf45-b-50-m/

---

# Problem Statement

The objective is to design a **continuous transparent protective enclosure** around the SF45/B.

A conventional solution might expose the LiDAR's optical path through a 320° slit/opening and use a mechanical support in the remaining sector.

That approach is undesirable for this application because:

1. The enclosure should visually appear continuous and symmetric.
2. A visible structural support or rear pillar would create an obvious obstruction.
3. A large 320° optical opening compromises the desired protective enclosure.
4. The enclosure should not visually reveal an obvious unsupported or obstructed sector.
5. The desired architecture is therefore a continuous transparent shell through which the LiDAR scans.

The design question becomes:

> **Can a transparent cylindrical/domed enclosure be placed around the SF45/B while keeping range accuracy, angular accuracy, detection probability, signal quality, and environmental performance within acceptable limits?**

---

# Design Requirements

## Primary Requirements

The enclosure should:

- Protect the LiDAR from accidental contact.
- Protect against minor impact.
- Reduce dust ingress.
- Reduce water/rain exposure.
- Provide a continuous transparent appearance.
- Avoid an obvious rear support pillar.
- Avoid a dedicated 320° slit if possible.
- Preserve the LiDAR's useful scanning field.
- Maintain acceptable ranging accuracy.
- Maintain acceptable angular accuracy.
- Maintain acceptable detection range.
- Avoid significant ghost returns.
- Avoid excessive optical attenuation.
- Remain mechanically stable.

## Secondary Requirements

Where practical, the enclosure should also:

- Resist scratches.
- Resist UV degradation.
- Resist condensation.
- Resist water adhesion.
- Maintain optical properties over temperature.
- Avoid excessive heat buildup.
- Be manufacturable.
- Be serviceable and cleanable.

---

# Proposed Enclosure Concept

A conceptual enclosure is a **continuous transparent dome or cylindrical/domed shell** mounted from the base.

```text
                 TRANSPARENT DOME
              _____________________
           .-'                     '-.
         .'                           '.
        /                               \
       |                                 |
       |             SF45/B              |
       |             ┌────┐              |
       |             │    │              |
       |             │    │              |
       |             └────┘              |
       |                                 |
       |                                 |
        \                               /
         '.                           .'
           '-._____________________.-'
                     BASE
```

The enclosure should ideally have:

- No rear optical slit.
- No visually obvious pillar through the scan sector.
- A rigid base.
- A continuous optical shell.
- Adequate clearance between the sensor and shell.

---

# Optical Phenomena

The protective enclosure changes the optical path from:

```text
LiDAR → air → target → air → receiver
```

to:

```text
LiDAR
  ↓
air
  ↓
protective material
  ↓
air
  ↓
target
  ↓
air
  ↓
protective material
  ↓
air
  ↓
receiver
```

The enclosure must therefore be treated as an **optical component**.

## 1. Refraction

At an air/material boundary:

\[
n_1\sin(\theta_1)=n_2\sin(\theta_2)
\]

Potential effects:

- Beam angular deviation
- Angular measurement error
- Apparent target-position error
- Range/geometry distortion
- Scan-angle-dependent errors

For a curved enclosure, the surface normal changes with position, so:

\[
\Delta\theta=f(\theta)
\]

rather than necessarily being constant.

---

## 2. Surface Reflection

Some optical energy is reflected at every material interface.

At normal incidence, an approximate Fresnel reflection is:

\[
R=\left(\frac{n_1-n_2}{n_1+n_2}\right)^2
\]

Potential effects:

- Reduced transmitted power
- Reduced return signal
- Ghost returns
- Near-field artifacts
- Background optical energy

---

## 3. Internal Reflection

Light can reflect between the inner and outer surfaces of the enclosure.

Possible consequences:

- False measurements
- Ghost points
- Spurious near-range returns
- Increased noise
- Receiver background

---

## 4. Multipath

The enclosure can create multiple optical paths.

For a time-of-flight system, different path lengths may appear as different ranges.

Potential effects:

- False range
- Multiple apparent returns
- Ambiguous measurements
- Increased range variance

---

## 5. Scattering

Scattering can result from:

- Surface roughness
- Scratches
- Dust
- Manufacturing imperfections
- Material inclusions
- Water droplets
- Condensation
- Haze
- Coatings

Potential effects:

- Stray light
- Reduced signal-to-noise ratio
- False detections
- Reduced maximum range

---

## 6. Absorption

The enclosure material absorbs some 905 nm energy.

Because the beam passes through the enclosure on both outgoing and return paths, material loss is effectively a double-pass problem.

If the transmission per pass is \(T\):

\[
T_{roundtrip}\approx T^2
\]

before considering other losses.

---

## 7. Thickness Variation

If enclosure thickness varies:

\[
t=t(\theta,\phi)
\]

then optical behavior can vary around the enclosure.

Potential effects:

- Position-dependent refraction
- Position-dependent attenuation
- Position-dependent reflection
- Scan-dependent calibration errors

---

## 8. Curvature Errors

Manufacturing imperfections can introduce:

- Eccentricity
- Waviness
- Uneven curvature
- Local deformation
- Molding defects

These can cause angle-dependent beam deviations.

---

## 9. Optical Wedge Effect

If the inner and outer surfaces are not locally parallel, the material behaves like an optical wedge.

For small wedge angle \(\alpha\):

\[
\delta\approx(n-1)\alpha
\]

This can introduce systematic angular error.

---

## 10. Dispersion

Refractive index can depend on wavelength:

\[
n=n(\lambda)
\]

This is likely secondary for a nominally single-wavelength 905 nm LiDAR but should still be considered during material selection.

---

## 11. Polarization Effects

Reflection and transmission can modify polarization.

Potential causes include:

- Fresnel effects
- Surface coatings
- Stress birefringence
- Manufacturing stress

Likely secondary unless the sensor's receiver is polarization-sensitive.

---

## 12. Stress Birefringence

Transparent polymers may develop optical anisotropy due to:

- Injection molding
- Mechanical stress
- Mounting pressure
- Thermal gradients

This may affect polarization and optical behavior.

---

# Environmental Effects

The enclosure must be evaluated not only when clean and dry, but under realistic outdoor conditions.

## 1. Dust

Dust can cause:

- Scattering
- Attenuation
- Surface contamination
- False returns
- Reduced range

Direct contamination of the enclosure may be more significant than atmospheric dust.

---

## 2. Rain

Rain affects the system through two different mechanisms.

### Atmospheric rain

Droplets between the LiDAR and target can cause scattering and attenuation.

### Rain on the enclosure

Water droplets on the enclosure can cause:

- Refraction
- Reflection
- Scattering
- Focusing/defocusing
- Attenuation

---

## 3. Water Film

A continuous water layer adds additional optical interfaces:

```text
air → water → enclosure → air
```

instead of:

```text
air → enclosure → air
```

Potential effects:

- Additional reflections
- Refraction
- Scattering
- Attenuation
- Angle-dependent errors

---

## 4. Fog

Fog contains suspended water droplets that scatter 905 nm radiation.

Potential effects:

- Atmospheric attenuation
- Backscatter
- False near-range returns
- Reduced target signal
- Reduced detection range

Fog-related degradation should be separated into:

1. Atmospheric degradation.
2. Additional enclosure-induced degradation.

---

## 5. Condensation

Condensation can form when the enclosure temperature falls below the dew point.

Potential effects:

- Haze
- Scattering
- Reduced transmission
- Ghost returns
- Reduced range

Temperature transitions should be tested, not only steady-state temperatures.

---

## 6. Snow

Potential effects:

- Scattering
- Attenuation
- Transient returns
- Surface accumulation
- Optical blockage

---

## 7. Smoke

Smoke particles can:

- Scatter 905 nm radiation.
- Absorb some energy.
- Reduce detection range.
- Increase background returns.

---

## 8. Atmospheric Aerosols / Pollution

Fine particulate matter can cause additional:

- Scattering
- Absorption
- Atmospheric extinction

This can be relevant in industrial, construction, dusty, and urban environments.

---

# Sunlight

The SF45/B is designed for operation in bright sunlight, and LightWare states that the sensor can operate in direct sunlight.

However, adding a transparent enclosure can change the optical environment.

## Potential sunlight-related effects

- Additional background optical energy
- Reflection from the enclosure
- Internal scattering
- Localized reflections
- Increased receiver background
- Reduced signal-to-noise ratio

The enclosure should therefore be tested under direct sunlight rather than assuming the bare sensor's performance automatically remains unchanged.

---

# Sun Glint and Reflective Targets

Particularly challenging targets include:

- Glass
- Polished metal
- Mirrors
- Water
- Glossy surfaces
- Vehicle bodies
- Reflective road signs

These can produce strong specular reflections.

The enclosure introduces additional reflective surfaces into the optical path.

---

# Target Reflectivity

Testing should include multiple target types:

- White matte target
- Grey matte target
- Black target
- Concrete
- Asphalt
- Vegetation
- Dark clothing
- Glass
- Polished metal
- Reflective material

The 50 m maximum range should not be assumed for every target type.

---

# Mechanical and Thermal Effects

## Mechanical Vibration

Potential sources:

- Vehicle vibration
- UAV vibration
- Motors
- Fans
- Scanning mechanism
- Wind
- Structural resonance

Potential effects:

- Point-cloud jitter
- Range jitter
- Angular jitter
- Time-varying optical geometry

---

## Wind Loading

A large dome can experience aerodynamic forces.

Potential effects:

- Structural vibration
- Enclosure movement
- Sensor movement
- Optical geometry variation

---

## Thermal Expansion

For a polymer:

\[
D(T)=D_0(1+\alpha\Delta T)
\]

Changes in:

- Diameter
- Curvature
- Thickness
- Mounting stress

can affect optical geometry.

---

## Heat Buildup

A sealed enclosure can change the thermal environment around the sensor.

Potential problems:

- Increased internal temperature
- Reduced convection
- Temperature gradients
- Condensation during cooldown
- Material deformation

The enclosure must preserve appropriate heat dissipation.

---

# Optical Material Requirements

The most important material properties are those at **905 nm**, not merely visible transparency.

The candidate material should have known:

| Property | Requirement |
|---|---|
| Transmission at 905 nm | High |
| Refractive index at 905 nm | Known |
| Absorption at 905 nm | Low |
| Scattering | Low |
| Surface quality | High |
| Thickness uniformity | High |
| UV resistance | Appropriate for deployment |
| Scratch resistance | Appropriate |
| Impact resistance | Appropriate |
| Temperature stability | Appropriate |
| Water resistance | Appropriate |

The supplier should ideally provide transmission data at or around 905 nm for the **actual material and thickness**.

---

# Candidate Materials

## Polycarbonate

### Advantages

- High impact resistance
- Lightweight
- Good mechanical protection
- Suitable for protective housings

### Concerns

- Refractive index
- 905 nm transmission
- Surface reflection
- Scratching
- UV degradation
- Manufacturing stress
- Optical homogeneity

---

## PMMA / Acrylic

### Advantages

- High optical clarity
- Good surface finish
- Easy to machine
- Good transparency

### Concerns

- Lower impact resistance than polycarbonate
- Scratching
- UV/environmental durability
- 905 nm transmission must be verified

---

## Optical Glass

### Advantages

- Excellent optical quality
- High scratch resistance
- Stable optical properties
- Potentially low optical distortion

### Disadvantages

- Higher mass
- More fragile
- More difficult/expensive manufacturing

---

# Flat Window vs Curved Dome

## Flat Window

```text
       ┌───────────────┐
       │ transparent   │
       │    window     │
       └───────────────┘
             LiDAR
```

### Advantages

- Simple manufacturing
- Easy to characterize
- Predictable geometry

### Disadvantages

- Large incidence-angle variation
- Potentially strong reflection/refraction
- Difficult to cover a very large FOV cleanly

---

## Curved Dome

```text
       ╭───────────────╮
      /                 \
     |       LiDAR       |
      \                 /
       ╰───────────────╯
```

### Advantages

- Continuous mechanical protection
- Symmetric appearance
- Large angular coverage
- No obvious optical slit

### Disadvantages

- More complex ray geometry
- Angle-dependent refraction
- Angle-dependent reflection
- Manufacturing tolerances matter
- May require calibration

---

# Calibration Strategy

The key question is whether enclosure-induced errors are **deterministic** or **stochastic**.

## Deterministic effects

Examples:

- Fixed dome geometry
- Refraction
- Thickness variation
- Fixed surface reflection
- Curvature errors

These may be characterized and calibrated.

Potential correction models:

\[
R_{corrected}=f(R_{measured},\theta,T)
\]

\[
\theta_{corrected}=g(\theta_{measured},T)
\]

A lookup table may also be used:

\[
LUT(\theta,\phi)
\]

---

## Stochastic effects

Examples:

- Rain droplets
- Changing dust
- Fog
- Condensation
- Random scattering
- Surface contamination

These generally cannot be completely removed through fixed calibration.

They must instead be minimized through:

- Material selection
- Surface treatment
- Geometry
- Cleaning
- Environmental control
- Heating/anti-condensation measures
- Operating limits

---

# Experimental Validation Plan

The enclosure should be validated against a **bare-LiDAR baseline**.

The same measurements should be performed:

1. Without enclosure.
2. With clean enclosure.
3. With environmentally contaminated enclosure.

---

## Test A — Range Accuracy

Test target distances:

- 1 m
- 2 m
- 5 m
- 10 m
- 20 m
- 30 m
- 40 m
- 50 m if practical

Measure:

\[
R_{bare}
\]

and:

\[
R_{dome}
\]

Calculate:

\[
\Delta R=R_{dome}-R_{bare}
\]

---

## Test B — Angular Accuracy

Use a large flat wall.

Measure the wall geometry without the enclosure.

Repeat with the enclosure.

Calculate:

\[
\Delta\theta(\theta)
\]

Determine whether the error is:

- Constant
- Linear
- Nonlinear
- Symmetric
- Asymmetric
- Repeatable

---

## Test C — Full Scan

Perform a complete scan over the configured angular range.

Plot:

\[
\Delta R(\theta)
\]

and:

\[
\Delta\theta(\theta)
\]

This is one of the highest-priority tests.

---

## Test D — Target Reflectivity

Test:

- White
- Grey
- Black
- Concrete
- Asphalt
- Vegetation
- Glass
- Metal

Compare:

- Detection probability
- Range
- Range variance
- False-return rate

---

## Test E — Direct Sunlight

Test:

1. Indoor
2. Outdoor shade
3. Bright daylight
4. Direct sunlight
5. Multiple sensor orientations relative to the sun

Compare bare and enclosed sensor performance.

---

## Test F — Rain

Test:

1. Dry enclosure
2. Light droplets
3. Continuous water film
4. Heavy rain
5. Water droplets at different positions

Measure:

- False points
- Dropouts
- Range error
- Noise
- Detection probability

---

## Test G — Fog

Test:

1. Clear air
2. Light fog
3. Medium fog
4. Dense fog

Measure:

- Detection range
- False returns
- Signal stability
- Noise

---

## Test H — Dust

Test:

1. Clean
2. Light dust
3. Moderate dust
4. Heavy dust

Then clean the enclosure and repeat the baseline measurement.

---

## Test I — Condensation

Create controlled condensation on:

- Inside surface
- Outside surface

Measure:

- Range
- Noise
- False returns
- Detection probability

Also test warm-to-cold transitions.

---

## Test J — Scratches / Aging

Compare:

- New enclosure
- Light scratches
- Moderate scratches
- UV-aged material if required

---

## Test K — Temperature

Measure performance across the expected operating temperature range.

Calculate:

\[
\Delta R(T)
\]

and:

\[
\Delta\theta(T)
\]

Separate enclosure effects from normal sensor temperature effects.

---

## Test L — Mechanical Vibration

Test the complete assembly under representative vibration.

Measure:

- Range jitter
- Angular jitter
- Point-cloud stability
- Enclosure movement

---

# Acceptance Criteria

The final acceptance limits should be defined according to the actual application.

Suggested categories:

| Metric | Bare LiDAR | Enclosed LiDAR | Allowed Change |
|---|---:|---:|---:|
| Range bias | Baseline | Measure | TBD |
| Range standard deviation | Baseline | Measure | TBD |
| Angular error | Baseline | Measure | TBD |
| Detection probability | Baseline | Measure | TBD |
| Maximum range | Baseline | Measure | TBD |
| False-return rate | Baseline | Measure | TBD |
| Point-cloud jitter | Baseline | Measure | TBD |
| Environmental degradation | Baseline | Measure | TBD |

The values marked `TBD` must be defined from the application's actual requirements.

---

# Priority of Investigations

A practical order for the engineering work is:

### Priority 1 — Optical transmission at 905 nm

Determine whether the candidate material introduces unacceptable attenuation.

### Priority 2 — Angular distortion

Determine whether the dome changes the apparent scan geometry.

### Priority 3 — Ghost/multipath behavior

Determine whether enclosure reflections produce false measurements.

### Priority 4 — Range accuracy

Compare enclosed and bare sensor measurements.

### Priority 5 — Rain/water

Determine how droplets and water films affect performance.

### Priority 6 — Dust/contamination

Determine performance degradation with surface contamination.

### Priority 7 — Sunlight

Determine whether the enclosure creates additional background/reflection problems.

### Priority 8 — Condensation

Determine whether thermal cycling creates optical fogging.

### Priority 9 — Mechanical/thermal stability

Verify the enclosure doesn't introduce vibration or thermal problems.

---

# Questions for Optical/LLM Analysis

The following questions can be given to an optical engineer or another LLM.

## Optical Geometry

1. For a 905 nm single-beam oscillating LiDAR with up to 320° scan, which enclosure geometry minimizes angular distortion?
2. Compare spherical, cylindrical, hemispherical, and flat-window designs.
3. Derive the ray path through:
   \[
   air\rightarrow polymer\rightarrow air
   \]
4. Determine angular error as a function of scan angle.
5. Determine how dome radius affects angular error.
6. Determine how dome radius affects range error.
7. Determine how material thickness affects beam displacement.
8. Determine the impact of inner/outer surface curvature.
9. Analyze optical wedge effects.
10. Determine whether a particular dome geometry can be ray-traced accurately enough for calibration.

## Material

11. Which transparent materials are suitable at 905 nm?
12. Compare polycarbonate, PMMA, optical glass, and other suitable materials.
13. Compare refractive index at 905 nm.
14. Compare transmission at 905 nm.
15. Compare absorption and scattering.
16. Compare UV resistance.
17. Compare scratch resistance.
18. Compare impact resistance.
19. Compare thermal stability.

## Surface Treatment

20. Can an anti-reflection coating optimized for 905 nm significantly reduce Fresnel losses?
21. Can hydrophobic coatings reduce water-induced degradation?
22. Can oleophobic coatings reduce contamination?
23. How durable are these coatings outdoors?

## Environmental Effects

24. Quantify rain effects.
25. Quantify water-film effects.
26. Quantify fog effects.
27. Quantify dust effects.
28. Quantify condensation effects.
29. Quantify sunlight effects.
30. Quantify smoke/aerosol effects.
31. Determine which environmental effect is likely to dominate in practical operation.

## Calibration

32. Can deterministic dome-induced errors be corrected?
33. What calibration procedure should be used?
34. Should calibration be:
   - Angle-only?
   - Range-only?
   - Angle + range?
   - Angle + range + temperature?
35. Would a lookup table be sufficient?
36. How frequently should calibration be repeated?

## Mechanical Design

37. What dome thickness provides sufficient impact resistance without excessive optical loss?
38. What dome radius is mechanically and optically appropriate?
39. How should the dome be mounted?
40. How can vibration be minimized?
41. How can thermal expansion be accommodated?
42. How can condensation be prevented?

---

# Expected Deliverables

The final engineering solution should provide:

## A. Enclosure Geometry

- Overall dimensions
- Dome/cylinder diameter
- Height
- Dome radius
- Wall thickness
- LiDAR-to-dome distance
- Mounting arrangement

## B. Material Selection

- Recommended material
- Refractive index at 905 nm
- Transmission at 905 nm
- Absorption
- Scattering
- Environmental properties

## C. Optical Analysis

- Refraction
- Reflection
- Scattering
- Multipath
- Ghost returns
- Angular distortion
- Range error

## D. Environmental Analysis

- Rain
- Water droplets
- Water film
- Fog
- Dust
- Condensation
- Sunlight
- Temperature
- UV
- Scratches

## E. Experimental Validation

- Test setup
- Target distances
- Target types
- Environmental tests
- Measurement metrics
- Statistical analysis
- Acceptance criteria

## F. Calibration

- Angular correction
- Range correction
- Temperature correction
- Contamination handling

---

# Important Engineering Principle

The enclosure should be treated as part of the optical system:

\[
\boxed{
System =
LiDAR +
Transparent\ Enclosure +
Environment
}
\]

rather than:

\[
LiDAR + Protective\ Plastic
\]

The objective is **not necessarily to make the enclosure optically perfect**.

The practical objective is:

\[
\boxed{
\text{Protect the LiDAR while keeping enclosure-induced errors within the application's error budget.}
}
\]

A deterministic error may be acceptable if it is:

- Small
- Repeatable
- Characterizable
- Calibratable

Random environmental effects such as rain droplets, dust, condensation, and changing fog must instead be minimized through enclosure design and environmental mitigation.

---

# Important Note About the 320° / 360° Requirement

The SF45/B is officially specified by LightWare as a **320° scanning LiDAR**.

This repository therefore treats the desired continuous enclosure as a **mechanical/optical housing requirement**, not as evidence that the underlying sensor has a 360° measurement field.

Any external documentation should distinguish clearly between:

- The sensor's actual manufacturer-specified scanning capability.
- The visual/mechanical geometry of the protective housing.
- Any application-specific claim about system coverage.

---

# References

## LightWare SF45/B

Official product page:

https://lightwarelidar.com/shop/sf45-b-50-m/

## LightWare Resources

Official manuals, datasheets and CAD resources:

https://lightwarelidar.com/resources-active-manuals-datasheets/

https://lightwarelidar.com/resources-2d-3d-cad-files/

## Optical Protective-Window Background

Protective optical windows can introduce reflection, absorption, scattering and other optical effects that may affect LiDAR performance.

Example technical literature:

https://pmc.ncbi.nlm.nih.gov/articles/PMC10007460/

## LiDAR and Fog / Atmospheric Effects

Fog and atmospheric particles can produce scattering and attenuation of LiDAR radiation.

Example technical literature:

https://pmc.ncbi.nlm.nih.gov/articles/PMC13517271/

---

# Project Status

**Status:** Investigation / Concept Development

### Current objective

Design and experimentally validate a transparent protective enclosure for the LightWare SF45/B that provides robust mechanical/environmental protection while maintaining acceptable LiDAR performance.

### Next steps

- [ ] Obtain official SF45/B CAD geometry.
- [ ] Determine exact optical aperture geometry.
- [ ] Select candidate transparent materials.
- [ ] Obtain 905 nm optical-property data.
- [ ] Build simple material test coupons.
- [ ] Perform bare-vs-material baseline tests.
- [ ] Develop dome geometry.
- [ ] Perform ray-tracing analysis.
- [ ] Prototype enclosure.
- [ ] Perform full scan validation.
- [ ] Test rain/water.
- [ ] Test dust.
- [ ] Test condensation.
- [ ] Test sunlight.
- [ ] Test temperature.
- [ ] Test vibration.
- [ ] Develop calibration model.
- [ ] Define final acceptance criteria.
- [ ] Produce final enclosure design.

---

## Disclaimer

This document is an engineering research brief, not a validated optical design. Actual enclosure performance must be established experimentally for the selected material, geometry, thickness, surface treatment, and operating environment.

