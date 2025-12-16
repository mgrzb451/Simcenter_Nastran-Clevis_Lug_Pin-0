# Simcenter Nastran - Lug Clevis Pin Study

After months of theory it's finally time for some practical projects. Let's go!

We'll be analyzing a mini assembly consisting of a Lug, a Clevis connected with a Pin. We'll perform 3 subcases comparing a fully 3D meshed assembly with the Pin meshed with 1D beam elements connected via RBE2 rigid elements and then RBE3 interpolated elements.

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/3dmodel.jpg" />

# 3D Mesh - the Control Case

We'll utilize the Symmetry Constraint to decrease computation time

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/half3d.jpg" />

## Results

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/full3D_result.gif" />

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/3ddisp.jpg" />

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/3dstress.jpg" />

# 1D Pin Mesh with RBE3

The Pin is meshed using 1D CBEAM elements connected to the Clevis and Lug with the interpolated RBE3 type elements. 

## Free-Free Modal Analysis

First we verify the integrity of the assembly fem by performing a Free-Free Modal Analysis. This took so long to solve on my *vintage* PC 😢

### Results

We can see from the Rigid Body Modes that the assembly is not defined correctly - need to fix it!

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/33_modal_wrong.gif" />

## Linear Static Analysis

Same boundary conditions and loads are applied.

### Results

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/rbe3disp.jpg" />

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/rbe3stress.jpg" />

# 1D Pin Mesh with RBE2

The Pin is meshed using 1D CBEAM elements connected to the Clevis and Lug with rigid RBE2 elements. Same boundary conditions and loads are applied

## Results

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/rbe2disp.jpg" />

<img src="https://github.com/mgrzb451/Simcenter_Nastran-Clevis_Lug_Pin-0/blob/main/assets/rbe2stress.jpg" />

# Conclusions

1. There isn't much difference between results in the Pin achieved with RBE2 and RBE3 elements. Both are however uncomfortably distant from the fully 3D meshed model with careful application of mesh refinement and Contact analysis which is treated as the control case
2. The deformations between the control case and the 1D Pin show a completely different shapes in the Pin
3. Based solely on this singular case study (which is not really a valid basis for any generalizations) representing pins as a 1D element can be treated as a simplification in a large assembly to be used with caution and when the result in the pin themselves are of no importance. But in that case it's just batter to do represent the connection itself with RBE-type elements
4. I need a new PC 😭
