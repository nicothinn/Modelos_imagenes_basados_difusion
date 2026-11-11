# Generación de imágenes con modelos de difusión

Proyecto académico de **Inteligencia Artificial Generativa** de la Universidad Autónoma de Occidente. Reúne cuatro notebooks sobre difusión para imágenes, visualización de Stable Diffusion y arquitecturas de generación de video.

> **Estado:** material experimental y educativo. Las métricas y muestras guardadas en los notebooks no constituyen una comparación controlada con resultados publicados.

## Notebooks

| Notebook | Contenido |
|---|---|
| [01 — MNIST y CIFAR-10](./01_Punto1_FINAL.ipynb) | Entrenamiento DDPM, generación y métricas exploratorias FID, IS, KID, precisión y recall. |
| [02 — Oxford Flowers](./02_Flowers_Chollet.ipynb) | Generación de flores con Keras y difusión; incluye una inferencia adicional de Stable Diffusion 3. |
| [03 — Visualización de Stable Diffusion](./03_SD_Visual.ipynb) | Latentes durante el denoising, componentes del pipeline y comparación latente/píxel. |
| [04 — Arquitecturas de video](./04_Video_SOTA.ipynb) | Explicación de arquitecturas, objetivos, evaluación y demo de CogVideoX. |

## Cómo ejecutarlos

Los notebooks están preparados para **Google Colab** y descargan datos o modelos durante la ejecución; no se incluyen datasets ni pesos en este repositorio.

1. Abre el notebook desde GitHub con **Open in Colab**, o descárgalo y súbelo a Colab.
2. Selecciona un runtime con GPU cuando el notebook lo requiera.
3. Ejecuta las celdas en orden. Cada notebook instala sus dependencias en sus primeras celdas.
4. Para modelos de Hugging Face que pidan autenticación, autoriza el modelo y guarda `HF_TOKEN` en **Colab Secrets**. Nunca pegues tokens en una celda ni los subas a GitHub.
5. Revisa los términos de uso de datasets y checkpoints antes de generar o redistribuir resultados.

No hay enlaces directos a sesiones de Colab: se abren desde los archivos del repositorio.

## Estado y limitaciones conocidas

- **Notebook 01:** la función de entrenamiento recorre una pasada del DataLoader por llamada; el argumento `steps` no equivale actualmente a 15 000 actualizaciones. Verifica el entrenamiento y vuelve a generar las métricas antes de reportar resultados. Algunas salidas guardadas pueden corresponder a una versión anterior del código.
- **Notebook 02:** el FID registrado usa 64 imágenes reales y 64 generadas; tómalo como una comprobación exploratoria, no como una estimación estable. El checkpoint está configurado para guardar el mejor modelo sin proporcionar `val_loss`.
- **Notebook 03:** verifica la escala del VAE al decodificar latentes intermedios y la autenticación del modelo en un runtime limpio antes de reutilizar las visualizaciones.
- **Notebook 04:** la demo genera un clip corto; ilustra el pipeline, pero no es un benchmark comparativo.
- Las métricas generativas dependen del número de muestras, del preprocesamiento y del extractor utilizado. No compares valores de notebooks distintos sin fijar ese protocolo.

El notebook 02 ocupa aproximadamente **33 MB** por sus salidas incrustadas. Antes de publicar, limpia outputs transitorios o conserva solo las visualizaciones necesarias. `.gitignore` no puede excluir contenido incrustado dentro de un `.ipynb`.

## Estructura prevista del repositorio

```text
README.md
.gitignore
01_Punto1_FINAL.ipynb
02_Flowers_Chollet.ipynb
03_SD_Visual.ipynb
04_Video_SOTA.ipynb
```

Los archivos de apoyo locales —enunciado, copias de papers, texto extraído, fragmentos de repositorios, cachés, datos, checkpoints y notas de trabajo— se excluyen del conjunto público mediante `.gitignore`; no se borran del equipo.

## Fuentes, Licencia y materiales de terceros

Las referencias académicas se identifican por título y arXiv ID en los notebooks; por ejemplo: [DDPM](https://arxiv.org/abs/2006.11239), [Latent Diffusion](https://arxiv.org/abs/2112.10752), [Stable Video Diffusion](https://arxiv.org/abs/2311.15127), [CogVideoX](https://arxiv.org/abs/2408.06072), [HunyuanVideo](https://arxiv.org/abs/2412.03603), [Wan](https://arxiv.org/abs/2503.20314), [LTX-Video](https://arxiv.org/abs/2501.00103) y [SANA-Video](https://arxiv.org/abs/2509.24695). No se redistribuyen aquí PDFs ni texto completo extraído.

Este proyecto no declara una licencia propia. Las licencias y condiciones de los datasets, modelos, checkpoints y fragmentos de terceros siguen siendo las de sus autores; verifica esos términos antes de reutilizarlos o redistribuirlos.
