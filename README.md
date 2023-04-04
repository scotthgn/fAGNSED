# fAGNSED
Broad-band  AGN SED model. Slight modification of AGNSED from Kubot &amp; Done (2018), in that it now allows a colour-temperature correction on the standard outer disc region. This code was used in Hagen \& Done (2023b, submitted) as a non-relativistic comparison to RELAGN. As it is based off (and very similar to) AGNSED, you should cite Kubota \& Done (2018) (https://ui.adsabs.harvard.edu/abs/2018MNRAS.480.1247K/abstract). Feel free to also cite Hagen \& Done (2023b, submitted).

Requirements
------------
* Working installation of HEASOFT (including XSPEC). This has been tested on Heasoft version 6.30, and 6.31, with XSPEC versions 12.12.1 and 12.13.0. If you do not already have Heasoft installed, it can be found here: https://heasarc.gsfc.nasa.gov/docs/software/heasoft/.


Installation
------------
1. Clone the repository
2. Compile the code (two methods): 
    * (Quick) Run the `compile_to_xspec.sh` shell script. This will pass the necessary compilation commands to Xspec such that you don't have to!
    * (Alterntive to 2.1): If you don't want to use the shell script then cd into the `src/` directory, open Xspec and type: `initpackage fagnsed lmod_fagnsed.dat .` .
3. Load model to Xspec. Again cd into the `src/` directory, open Xspec and type: `lmod fagnsed .`
4. (OPTIOANL): Make Xspec auto-load fagnsed upon startup. There are two methods for this:
    * (Quick): Run the `init_xspec_autoload.sh` shell script
    * (Alternative to 4.1): If you don't want to use the shell script you can instead cd into `~/.xspec` open your `xspec.rc` file (if it does not exist, you can make one!) and give it the following line: `lmod fagnsed /path/to/fAGNSED/src` 
    
    
Model Parameters
----------------
**Par 1. &ensp;  $M$** </br>
  &emsp; &emsp; &#9656; **Units:** $M\_{\odot}$ </br>
  &emsp; &emsp; &#9656; **Description:** Mass of the central Black Hole

**Par 2. &ensp;  $D$** </br>
  &emsp; &emsp; &#9656; **Units:** Mpc </br>
  &emsp; &emsp; &#9656; **Description:** Co-Moving distance from the observer to the Black Hole </br>
  
**Par 3. &ensp;  $\log \dot{m}$** </br>
  &emsp; &emsp; &#9656; **Units:** $\log \dot{M}/\dot{M}\_{\mathrm{Edd}}$ </br>
  &emsp; &emsp; &#9656; **Descripton:** Log Mass-accretion rate, scaled by the Eddington mass accretion-rate. 
  (i.e $\log \dot{m} = -1$ would imply $\dot{M} = 0.1 \dot{M}\_{\mathrm{Edd}}$)
 
 **Par 4. &ensp; $a$** </br>
  &emsp; &emsp; &#9656; **Units:** Dimensionless </br>
  &emsp; &emsp; &#9656; **Description:** Black hole spin parameter. 0 implies non-spinning, while 1 is maximally spinning (with prograde rotation). 
  Note, the code will limit you to max 0.998 - This is the theoretical maximum assuming the presence of a disc

 **Par 5. &ensp; $\cos(i)$** </br>
  &emsp; &emsp; &#9656; **Units:** Dimensionless </br>
  &emsp; &emsp; &#9656; **Description**: Cosine of the inclination of the observer with respect to the disc, as measured from the z-axis with 
  the disc in the x-y plane 
 
 **Par 6. &ensp; $kT\_{e, h}$** </br>
  &emsp; &emsp; &#9656; **Units:** keV </br>
  &emsp; &emsp; &#9656; **Description:** Electron temperature for the hot Comptonising corona. 
  This sets the high-energy roll-over for the hot Comptonisation region
 
 **Par 7. &ensp; $kT\_{e, w}$** </br>
  &emsp; &emsp; &#9656; **Units** keV </br>
  &emsp; &emsp; &#9656; **Description:** Electron temperature for the warm Comptonising region.
 
 **Par 8. &ensp; $\Gamma\_{h}$** </br>
  &emsp; &emsp; &#9656; **Units:** Dimensionless </br>
  &emsp; &emsp; &#9656; **Description:** Spectral index for the hot Comptonisation component
 
 **Par 9. &ensp; $\Gamma\_{w}$** </br>
  &emsp; &emsp; &#9656; **Units:** Dimensionless </br>
  &emsp; &emsp; &#9656; **Description:** Spectral index for the warm Comptonisation component
 
 **Par 10. &ensp; $r_{h}$** </br>
  &emsp; &emsp; &#9656; **Units:** $R\_{G}$ ( $R\_{G} = GM/c\^{2}$ so technically dimensionless) </br>
  &emsp; &emsp; &#9656; **Description:** Outer radius of the hot Corona. 
  If this is negative, then the code will set it to the innermost stable cirbular orbit, $r\_{\mathrm{isco}}$
 
 **Par 11. &ensp; $r_{w}$** </br>
  &emsp; &emsp; &#9656; **Units:** $R\_{G}$ </br>
  &emsp; &emsp; &#9656; **Description:** Outer radius of the warm Comptonisation region. 
  If this is negative, then the code will set it to $r\_{\mathrm{isco}}$
 
 **Par 12. &ensp; $\log r\_{\mathrm{out}}$** </br>
  &emsp; &emsp; &#9656; **Units:** $R\_{G}$ </br>
  &emsp; &emsp; &#9656; **Description:** Log of the outermost disc radius. 
  If this is negative, then the code will use the self-gravity radius from Laor &amp; Netzer (1989)
 
 **Par 13. &ensp; $f\_{\mathrm{col}}$** </br>
  &emsp; &emsp; &#9656; **Units:** Dimensionless </br>
  &emsp; &emsp; &#9656; **Description:** Colour-temperature correction to be applied to the standard **outer* disc. 
  If this is negative, then the code follows the relation in Done et al. (2012). Otherwise treated as a constant correction
 
 **Par 14. &ensp; $h\_{\mathrm{max}}$** </br>
  &emsp; &emsp; &#9656; **Units:** $R\_{G}$ </br>
  &emsp; &emsp; &#9656; **Description:** Maximum scale-height of the inner-corona
 
 **Par 15. &ensp; $z$** </br>
  &emsp; &emsp; &#9656; **Units:** Dimensionless </br>
  &emsp; &emsp; &#9656; **Description:** Redshift of the source
 
 </br>
