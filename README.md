# Generación de imágenes y video con modelos de difusión

Proyecto académico de **Inteligencia Artificial Generativa** de la Universidad Autónoma de Occidente. Reúne cuatro notebooks sobre difusión para imágenes, visualización de Stable Diffusion y arquitecturas de video, más el documento del punto 4.

> **Estado:** puntos 1, 2, 3 y 4 ejecutados y documentados. Falta el video de la exposición.

## Notebooks

| Notebook | Contenido | Abrir en Colab |
|---|---|---|
| 01 — MNIST y CIFAR-10 | DDPM con diffusers, 15000 pasos por dataset, FID/KID/precisión/recall | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicothinn/Modelos_imagenes_basados_difusion/blob/main/01_Punto1_FINAL.ipynb) |
| 02 — Oxford Flowers | Ejecutado: difusión Keras 128x128, 80 épocas, FID 156.7 con 1000 imágenes | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicothinn/Modelos_imagenes_basados_difusion/blob/main/02_Flowers_Chollet.ipynb) |
| 03 — Visualización de Stable Diffusion | Ejecutado: latentes 64x64 vs píxel 512x512, texto CLIP y proceso de denoising | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicothinn/Modelos_imagenes_basados_difusion/blob/main/03_SD_Visual.ipynb) |
| 04 — Arquitecturas de video | Ejecutado: arquitecturas, evaluación y demo de CogVideoX | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicothinn/Modelos_imagenes_basados_difusion/blob/main/04_Video_SOTA.ipynb) |

## Resultados del punto 1

Protocolo: **1000 imágenes generadas contra 1000 del test**, 32x32, características Inception-v3. FID, KID, precisión y recall con `torch-fidelity`.

| Dataset | FID ↓ | KID ↓ | Precisión ↑ | Recall ↑ | F-score ↑ |
|---|---|---|---|---|---|
| MNIST | 32.9 | 0.023 | 0.588 | 0.740 | 0.655 |
| CIFAR-10 | 91.1 | 0.040 | 0.781 | 0.345 | 0.479 |

`clean-fid` da 31.1 en MNIST y 95.4 en CIFAR-10; se usa como comprobación, no como protocolo principal. Los valores no son comparables con papers que usan 50000 muestras u otro extractor.

## Resultado del punto 2

El notebook 02 está ejecutado con 80 épocas. El FID con 1000 imágenes generadas y 1000 reales es **156.7**. Las muestras pasan de manchas de color a flores reconocibles, con textura de acuarela; no son fotorrealistas. El modelo tiene 1.9 millones de parámetros y trabaja a 128x128, así que el número no es comparable con papers que usan modelos y muestras mucho mayores.

## Resultado del punto 3

El notebook 03 está ejecutado. Muestra el latente de 64x64 y el píxel de 512x512 en seis momentos del denoising (0, 10, 20, 30, 40 y 50), con el factor de escala del VAE aplicado antes de decodificar. La imagen final y el panel de evolución quedaron guardados en el notebook.

## Documento del punto 4

- [Word](./docs/Documento_Punto4_Arquitecturas_Video.docx)
- [PDF](./docs/Documento_Punto4_Arquitecturas_Video.pdf)

El documento cubre representación de video, U-Net 3D, cascadas, difusión latente, DiT/MM-DiT, objetivos de entrenamiento, condicionamiento, video largo, eficiencia, FVD, VBench, tabla comparativa y demo de CogVideoX-2B.

El notebook 04 también está ejecutado: la demo de CogVideoX-2B generó 33 fotogramas a 720x480, 20 pasos y guidance 6.0, y guardó el clip y el panel de fotogramas. La demo es ilustrativa y no un benchmark.

## Cómo ejecutarlos

Los notebooks están preparados para **Google Colab**. Descárgalos o ábrelos con el badge y selecciona un runtime con GPU T4.

1. Ejecuta las celdas en orden. Cada notebook instala sus dependencias en las primeras celdas.
2. Para modelos que pidan autenticación, agrega `HF_TOKEN` en **Colab Secrets**. No pegues tokens en una celda ni los subas al repositorio.
3. Revisa los términos de datasets y checkpoints antes de redistribuir resultados.
4. El 01 y el 02 guardan checkpoints durante el entrenamiento; si Colab se reinicia, revisa la ruta antes de volver a entrenar.

## Estado y limitaciones

- **01:** entrenado con 15000 pasos en MNIST y CIFAR-10. DPM-Solver se excluyó de la comparación porque no convergió con este modelo y 20 pasos.
- **02:** ejecutado: 80 épocas y FID de 156.7 con 1000 imágenes. Las muestras son flores reconocibles, no fotorrealistas; el modelo es pequeño (1.9M de parámetros).
- **03:** ejecutado: latente 64x64 contra píxel 512x512 en seis pasos, con el factor de escala del VAE corregido (`0.18215`). La imagen final y el panel de evolución están en el notebook.
- **04:** documento y demo ejecutados. La demo de CogVideoX-2B ilustra el pipeline y no es un benchmark.
- Las métricas generativas dependen del número de muestras, el preprocesamiento y el extractor. No compares valores de notebooks distintos sin fijar el protocolo.

## Estructura del repositorio

```text
README.md
01_Punto1_FINAL.ipynb
02_Flowers_Chollet.ipynb
03_SD_Visual.ipynb
04_Video_SOTA.ipynb
docs/
  Documento_Punto4_Arquitecturas_Video.docx
  Documento_Punto4_Arquitecturas_Video.pdf
```

Los archivos de apoyo locales —datasets, pesos, checkpoints, historiales y notas de trabajo— se excluyen mediante `.gitignore` y no se distribuyen.

## Fuentes, licencia y materiales de terceros

Las referencias académicas se identifican por título y arXiv ID en los notebooks y en el documento; por ejemplo: [DDPM](https://arxiv.org/abs/2006.11239), [Latent Diffusion](https://arxiv.org/abs/2112.10752), [CogVideoX](https://arxiv.org/abs/2408.06072), [HunyuanVideo](https://arxiv.org/abs/2412.03603), [Wan](https://arxiv.org/abs/2503.20314), [LTX-Video](https://arxiv.org/abs/2501.00103) y [SANA-Video](https://arxiv.org/abs/2509.24695). No se redistribuyen PDFs ni texto completo extraído.

Este proyecto no declara una licencia propia. Las licencias y condiciones de los datasets, modelos, checkpoints y fragmentos de terceros siguen siendo las de sus autores; verifica esos términos antes de reutilizarlos o redistribuirlos.
