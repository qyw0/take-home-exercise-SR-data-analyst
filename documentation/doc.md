## computeLighting

This event captures the Editor performing any kind of lighting bake (light probes, Enlighten realtime GI, progressive lightmapper, etc).

| Parameter | Description |
| --- | --- |
| duration | The total time between the bake operation beginning and ending. \*\*\* When lighting is being &#39;auto generated&#39;, the beginning of the bake is taken to mean the point at which any actual data update task begins to happen (GIPreprocessManager::EnterStage / PVRScopedProgress). The end of the bake is when there are no further outstanding jobs. |
| blocking | Lighting computation is usually run in the background, in which case this is false. However, there are some scenarios in which it happens synchronously, such as during the build process; in this situation it will be true. |
| parameters.autoGenerate | True if the bake is beginning due to &#39;Auto Generate&#39; lightmaps mode initiating the bake; false if the bake was initiated manually (via the UI or API). |
| parameters.sourceView | The name of the GUIView that was active / processing events when the bake was initiated, if any. This will usually tell us that the bake was started via the lighting window, but might also help us track usage of Editor extensions which provide an interface to the lighting system. If this is missing, no GUIView was active when the bake started. |
| parameters.bakeBackend | The lightmapping backend used for the bake: either **enlighten** or **progressivecpu**. |
| parameters.computeRealtime | True if realtime GI is enabled, false otherwise. |
| parameters.computeBaked | True if baked GI is enabled, false otherwise. |
| parameters.outcome | The result of the baking process:\*\*\* **success** : the bake completed successfully.\*\*\ ***cancelled** : the bake was explicitly cancelled, either via the UI or API.\*\*\ ***forcestop** : the bake was &#39;force stopped&#39;, which only applies to the progressive lightmapper. \*\*\* **interrupted** : the bake event was ended because the bake settings changed. A new bake event should immediately follow this one with the new settings. |

## Realtime GI parameters - omitted if Realtime GI is not enabled
| Parameter | Description |
| --- | --- |
| parameters.indirectResolution | The value of the &#39;Indirect Resolution&#39; lightmapping parameter. |

## Baked GI parameters - omitted if Baked GI is not enabled
|.|.|
| --- | --- |
| parameters.lightmapResolution | The value of the &#39;Lightmap Resolution&#39; lightmapping parameter. |
| parameters.compressLightmaps | True if the &#39;Compress Lightmaps&#39; flag is enabled, false otherwise. |
| parameters.lightmapSize | The value set for &#39;Lightmap Size&#39; |
| Final Gather parameters - omitted if Final Gather is not enabled |
| parameters.enlighten.finalGather.rayCount | If Final Gather is enabled, the number of rays it is set to use. |
| parameters.enlighten.finalGather.denoise | True if Denoising is enabled for Final Gather, false otherwise. |
| Ambient Occlusion parameters - omitted if Ambient Occlusion and Baked GI are not enabled |
| parameters.ambientOcclusion.maxDistance | The maximum distance value for computing Ambient Occlusion rays. |
| Progressive Lightmapper parameters - omitted if not using the progressive lightmapper |
| parameters.progressive.directSamples | The number of direct samples specified for the progressive lightmapper. |
| parameters.progressive.indirectSamples | The number of indirect samples specified for the progressive lightmapper. |
| parameters.progressive.bounces | The number of bounces specified for the progressive lightmapper. |
| parameters.progressive.prioritizeView | True if the &#39;prioritize view&#39; box is checked for the progressive lightmapper, false otherwise. |
