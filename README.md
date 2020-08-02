# Trials Of Mana Shaders

![Primary Shading Function](https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/MF_ShadingBase.png)

Reverse engineered UE4 shaders from Trials of Mana. Contents include:

- The full material graphs for clothing, skin, hair, and eye shaders
- Models and materials for the starting classes of each main character
- A relaxed pose animation for each model

Generated with **Unreal Engine 4.22.3**

These files are intended as a learning resource for technical artists, shader enthusiasts, or anyone interested in stylized/NPR graphics.

Note that while these material graphs are a close reproduction, they do not compile into the matching assembly code of the originals. I am not familiar enough with the Unreal Engine's material compiler to accomplish that.

## About the Shaders

![Shading Breakdown](https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/ShaderBreakdown.png)

Trials of Mana is one of a steadily expanding group of games that mix stylized cartoon rendering with Unreal Engine's PBR pipeline. While classical approaches to stylized rendering may use a cell-shading model or bake stylized lighting into the asset, these games use a mixed approach that allows the game to render stylized visuals while retaining the powerful lighting capabilities of physically based rendering.

Similar to standard PBR, Trials of Mana uses flat base colors, normal maps, and Metallic-Roughness-Specular parameters as inputs. However, in addition to the standard pipeline, a custom stylization function is used to apply several effects to the color inputs before the PBR lighting model gets applied.

Most the stylization function is implemented in *MF_ShadingBase* material function (graph shown above). However, not all materials use the function in its entirety.

These materials use the full *MF_ShadingBase* function:
- M_ch_BaseVer03
- M_ch_BaseVer03_ADD

These materials are heavily based on *MF_ShadingBase* or use parts of it:
- M_ch_BaseVer03_HairMatCap
- M_ch_Hair
- M_ch_Skin

These materials implement their own effects entirely:
- M_ch_Eye
- M_ch_EyeEx
- M_ch_Jewel
- M_ch_Tear

## Shader Effects

### Rim Shadows
Colored shadows applied relative to the camera's view direction. Applied to hair and clothing.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepRimShadows1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepRimShadows2.gif" width="20%" />
</span>

### Skin Shadows
Similar shading as above applied to skin. Uses a slightly different blending formula though.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepSkinShadows1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepSkinShadows2.gif" width="20%" />
</span>

### Specular Lighting
Single source specular lighting for metallic materials. Specular light source and color are controlled in the **MPC_DirectionalLight** parameter collection.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepSpecular1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepSpecular2.gif" width="20%" />
</span>

### Anistropic Specular
Specular lighting using anisotropic distribution. Uses the same light source as the regular Specular.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepAnisoSpecular1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepAnisoSpecular2.gif" width="20%" />
</span>

### Skin Specular
Specular lighting applied to skin. Like the other specular options, it is controlled via the **MPC_DirectionalLight** parameter collection.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepSkinSpecular1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepSkinSpecular2.gif" width="20%" />
</span>

### Cell Lighting
Graident mapped cell lighting applied relative to the specular light source. Primarily applied to skin and hair.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepCellLighting1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepCellLighting2.gif" width="20%" />
</span>

### Rim Lighting
Colored rim highlights applied relative to the camera's view direction. Only used for a very subtle skin highlight

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepRimLight1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepRimLight2.gif" width="20%" />
</span>

### Lighting Modulation
Color multiplied in at the very end of sytlization function. Defaults to 50% gray allowing the final color to be both lightened and darkened.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepEmissive1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/StepEmissive2.gif" width="20%" />
</span>

### SpecialFX Rim Lighting
Implemented in the *MF_FXRim* material function. Used to highlight characters and weapons during special attacks.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/FXRim1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/FXRim2.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/FXRim3.gif" width="30%" />
</span>

### SpecialFX Ghost Fresnel
Implemented in the *MF_GhostTranslucent* material function. Applies a ghostly glow to models. Also applies a slight dithered transparency around surface edges.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Ghost1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Ghost2.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Ghost3.png" width="20%" />
</span>

### SpecialFX Sihouette
Turns the model completely black. As the name implies, it is used to show only the sihouette of the character.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Silhouette1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Silhouette2.png" width="20%" />
</span>

### Custom Dither

Implemented in the *MF_CustomDither* material function. Works similar to the *DitheredTemporalAA* node except it exposes additional dither parameters. Varying the dither pattern can allow multiple dithered objects to overlap without obscuring each other.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/CustomDither1.png" width="30%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/CustomDither2.png" width="30%" />
</span>

### M_ch_Jewel
The jewel material applies a faceting effect. It also takes a color gradient used to emulate color diffraction over the surface of the material.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/JewelShader.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/JewelShaderModel.png" width="20%" />
</span>

### M_ch_Eye

The eye material takes 3 texture maps and composites them using fake parallax to give eyes the appearance of depth

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Eye1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Eye2.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Eye3.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/EyeShader.gif" width="20%" />
</span>

### MF_ColorID

A helpful material function allowing multi-channel color mapping to be enabled on-demand for any material using it. Inputs entering into the *IDMap*, *Channel G*, and *Channel B* ports do not get compiled as part of the material unless the **UsedGreenChannel** or **UsedBlueChannel** switches are active.

<img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/IDMapping.png" />

## Shader Parameters

| Static Switches          | |
| ------------------------ |-|
| **UseSpe**               | Enables specular lighting on the material                                                                |
| **UseAnisoSpe**          | Enables anisotropic specular lighting on the material                                                    |
| **UseGreenChannel**      | Enables a second material color channel mapped to the green channel of the IDMap texture                 |
| **UseBlueChannel**       | Enables a third material color channel mapped to the blue channel of the IDMap texture                   |

| Basic Parameters         | |
| ------------------------ |-|
| **BlackSiletSwitch**     | Enables SpecialFX Silhouette mode. Should be 0 or 1.                                                     |
| **ColorPow**             | A color adjustment parameter. Saturation decreases as it approaches 1.                                   |
| **Opacity**              | Material opacity                                                                                         |
| **Emi**                  | Color modulation parameter. Despite its name, it can be used to both light or darken the final color     |

| Anisotropic Specular     | |
| ------------------------ |-|
| **AnisoRoughnessX**      | X roughness parameter. Stretches the specular highlight horizontally                                     |
| **AnisoRoughnessY**      | Y roughness parameter. Stretches the specular highlight vertically                                       |
| **AnisoLightColor**      | The color of reflected light                                                                             |

| SpecialFX Rim Light      | |
| ------------------------ |-|
| **FXRim_Color**          | Color of the rim effect                            |
| **FXRim_Int**            | Intensity                                          |
| **FXRim_Range**          | Coverage                                           |
| **FXRim_Switch**         | Enables the SpecialFX Rim light. Should be 0 or 1. |

| SpecialFX Ghost Fresnel  | |
| ------------------------ |-|
| **GhAlphaTest**          | Alpha threshold for fringe transparency |
| **GhFresnel_Color**      | Color of the ghost effect               |
| **GhFresnel_Base**       | Lighting base                           |
| **GhFresnel_Exp**        | Lighting exponent                       |

| Custom Dither            | |
| ------------------------ |-|
| **Dither**               | Dithering factor |
| **x**                    | X offset         |
| **y**                    | Y offset         |

## Notes
These shaders were based off of the shaders in the Trials of Mana pre-release demo. As a result there may be differences between them and the final release versions. 

- The **M_ch_BaseVer03_HairMatCap** shader used for Riesz' hair does not properly darken when the **BlackSiletSwitch** parameter is active. This was verified against the original compiled shader from the demo's game files.
- The ID map textures for Charlotte's **wear01** and **wear02** materials are present, but unused. The material parameter set data does not reference them and the static switch enabling secondary color channels for these materials is disabled.

It is possible that the above two errors were fixed in the release version of the game. However, I have not taken the time to confirm.
