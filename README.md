# Flow Test Tower
3mf and models for a printer flow test tower

## What is this?
PrusaSlicer and SuperSlicer have some really great filament profiles with volumetric flow rates set per filament for E3D V6 hotends a little conservatively but the faster print profiles ride the flow rates quite aggressively. If you have a less well supported hotend, you should be able to dial in your maximum rates. Whilst you can check for when the extruder skips doing free extrusion, die swell issues happen way before this and a geared extruder with a fairly feeble pancake stepper is capable of blowing a PTFE tube up like a balloon. By printing this tower you can find the speeds at which die swell will badly distort your print.

## How to use
Open the 3mf for your slicer, load up your printer, filament under test and the quality profile you wish to use, make changes as shown in **Slicer Settings** below. Look at the [layers set up in the window on the right](images/layers.png) and check the speeds are sensible for your hotend and motion system, adjust if not. Consider a taller layer height (0.75 * nozzle width) and a slightly wider extrusion width (upto 1.5 * nozzle width) to get higher flow at lower speeds and exaggerate die shrink effects. Remember this will increase your volumentric flow rate so record that not the peak linear speed achieved.

Check the seam is painted on to one of the sharp corners. It will look awful, but we're suck on one perimeter without vase mode. Consider not using `retract on layer change`, `wipe` or `zhop` features. 

 Hit slice now and check the [linear speed changes at each step height](images/linear_spped.png). Check the [volumetric flow visualisation](images/filament_vol_speed.png), and take a screenshot, this will be what we take our measurements from.

## Interpreting Results
Ignore the sharp corners. Thy're there to attract seams. They should be painted on one of them. With multiple vertical shells you won't have artifacts here. If the extruder starts skipping steps, stop. If the print starts curling up badly that's the dreaded die shrink, stop. Measure the height of the failure. Cross referecne it to the volumetric flow visualisation we looked at earlier. Use the last good looing step on the tower as the new volumetric flow cap for that filament. Don't forget to change the cooling settings back before you save the filament profile. 

## Slicer Settings
- Filament Settings
  Use your regular profile for the filament under test with the following changes:
  - Filament (SuperSlicer)
    - Max Volumetric Speed: 99 (or some limit just above what the tower hits)
    - Max Speed: 0 (or something higher than the tower asks for, may be greyed out)
  - Advanced (PrusaSlicer)
    - Print Speed Override: 99 (or some limit just above what the tower hits)
  - Cooling
    - layer time goal: 0
- Print Settings
  Use your regular quality and layer height/width profile
  - Layers and Perimeters
    - Vertical Shells
      - Perimeters: 1
    - Horizontal Shells
      - Bottom: 3 (suggested, just to keep the model stuck)
      - Top: 0
  - Infill
    - Fill Density: 0%
  - Skirt and Brim
    -  A brim is recommended for ABS, you know your printer. 
  - Speed
    We override most of this, so just make sure four first layer, perimeter and solid infill settings are sane
    - Auto Speed
      - Max Print Speed: Set above what you set in the tower, this is enforced
      - Max Volumetric Speed:  99 (or some limit just above what the tower hits)
  - Machine Limits
    - Make sure you can achieve the speeds the tower requests.
    - TODO
  - TODO retract on layer / wipe
  
## FAQ
- Will you support Cura?
  - No. Not until cura supports volumetric flow caps and sensible separation of printer and filament settings from the quality intent profiles.
- Can you make a faster/slower version
  - Edit the speed changes at each layer yourself. Send me a PR. I might add more as I use them. 