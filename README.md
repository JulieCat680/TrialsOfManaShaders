# Trials Of Mana Shaders

![Primary Shading Function](https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/MF_ShadingBase.png)

Reverse engineered UE4 shaders from Trials of Mana. Contents include:

- The full material graphs for clothing, skin, hair, and eye shaders
- Models and materials for the starting classes of each main character
- A relaxed pose animation for each model

Generated with **Unreal Engine 4.22.3**

These files are intended as a learning resource for technical artists, shader enthusiasts, or anyone interested in stylized/NPR graphics.

Note that while these material graphs are a close reproduction, they do not compile into the matching assembly code of the originals. I am not familiar enough with the Unreal Engine's material compiler to accomplish that.

### About the Shaders

![Shading Breakdown](https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/ShaderBreakdown.png)

Trials of Mana is one of a steadily expanding group of games that mix stylized cartoon rendering with Unreal Engine's PBR pipeline. While classical approaches to stylized rendering may use a cell-shading model or bake stylized lighting into the asset, these games use a mixed approach that allows the game to render stylized visuals while retaining the powerful lighting capabilities of physically based rendering.

Similar to standard PBR, Trials of Mana uses flat base colors, normal maps, and Metallic-Roughness-Specular parameters as inputs. However, in addition to the standard pipeline, a custom stylization function is used to apply several effects to the color inputs before the PBR lighting model gets applied.

Most the stylization function is implemented in *MF_ShadingBase* material function (graph shown above). This function serves as the basis for most of the reverse-engineered materials provided:
- M_ch_BaseVer03
- M_ch_BaseVer03_ADD
- M_ch_BaseVer03_HairMatCap
- M_ch_Skin

M_ch_Skin is a bit different in that it uses Unreal's Preintegrated Subsurface Skin shading model, but most parts of the graph still come from the base shading function.

There are also a few materials that implement their own effects entirely:
- M_ch_Jewel
- M_ch_Eye

#### MF_ShadingBase

The base stylization function is responsible for applying several effects:
- Rim shading and lighting
- Base specular highlights
- Anisotropic-specular highlights
- Tone adjustment
- Gradient cell-shade light mapping
- Emissive lighting
- SpecialFX rim lighting
- SpecialFX ghost lighting
- SpecialFX black overlay for silhouetting
- Custom opacity dithering

##### TODO: Add examples of these effects

#### M_ch_Jewel
The jewel material applies a faceting effect. It also takes a color gradient used to emulate color diffraction over the surface of the material.

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/JewelShader.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/JewelShaderModel.png" width="20%" />
</span>

#### M_ch_Eye

The eye material takes 3 texture maps and composites them using fake parallax to give eyes the appearance of depth

<span>
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Eye1.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Eye2.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/Eye3.png" width="20%" />
  <img src="https://raw.githubusercontent.com/JasonL663/TrialsOfManaShaders/master/Images/EyeShader.gif" width="20%" />
</span>

### Notes
These shaders were based off of the shaders in the Trials of Mana pre-release demo. As a result there may be differences between them and the final release versions. 

- The **M_ch_BaseVer03_HairMatCap** shader used for Riesz' hair does not properly darken when the **BlackSiletSwitch** parameter is active. This was verified against the original compiled shader from the demo's game files.
- The ID map textures for Charlotte's **wear01** and **wear02** materials are present, but unused. The material parameter set data does not reference them and the static switch enabling secondary color channels for these materials is disabled.

It is possible that the above two errors were fixed in the release version of the game. However, I have not taken the time to confirm.
