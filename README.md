# Proyecto_RecSys

Recomendación de Recetas y Promoción de Alternativas Más Saludables: Un Estudio Comparativo entre Modelos Tradicionales y LLMs

El propósito de este proyecto es evaluar como los LLMs en configuraciones zero-shot y fine-tuned comparan con sistemas de recomendación más tradicionales para recomendar recetas, con un enfoque en dar recomendaciones más saludables usando métricas nutricionales.

# Metodología

La metodología consiste en lo siguente:

1. Modelos Tradicionales de Recomendación

2. LLMs en Zero-Shot

3. Fine-Tuning de un LLM local con LoRA

# Estructura del repositorio

```text
ProyectoRecSys/
│
├── plots/                        # Gráficos de evaluación y comparaciones
│
├── config.env                    # Variables de configuración local (paths, seeds)
├── pyproject.toml                # Dependencias (Poetry)
│
├── data_baselines.ipynb          # Métodos baselines clásicos de RecSys
│
├── rec_finetune_local.ipynb      # Primer intento de Fine-tuning principal (TinyLlama)
├── rec_finetune_local_phi2.ipynb # Fine-tuning para Phi-2
│
├── rec_zeroshot.ipynb            # Zero-shot usando API externa
├── rec_zeroshot_local.ipynb      # Zero-shot con modelos locales
├── rec_zeroshot_local_gemma.ipynb
├── rec_zeroshot_local_gemma1b.ipynb
│
├── recipes.csv                   # Dataset de recetas
└── reviews.csv                   # Dataset de reviews históricas
```

# Instalación y Config

Para hacer recomendaciones con LLMs grandes por la API de Google, hay que poner una llave válida en config.env, luego Copiar config.env como .env:

# Experimentos

Cómo correr los experimentos

1. Zero-Shot (modelos locales o API)

- rec_zeroshot.ipynb: Zero-shot usando API (si configuraste una).
- rec_zeroshot_local.ipynb: Zero-shot con modelos locales (Gemma, TinyLlama).
- rec_zeroshot_local_gemma*.ipynb: Experimentación con Gemma 2B y 1B.

Cada jupyter notebook procesa recetas, genera recomendaciones, y calcula el Health Score y las métricas generales.

2. Fine-Tuning (LoRA)

Los notebooks:

- rec_finetune_local.ipynb
- rec_finetune_local_phi2.ipynb

Realizan:

- Generación de dataset formal para SFT (train.jsonl, val.jsonl)
- Entrenamiento LoRA con PEFT
- Evaluación automática
- Exportación del modelo finetuned
- Merge final (para inferencia más rápida)

Los modelos resultantes quedan guardados en carpetas localmente, ya que son muy grandes para subirlas directo al repositorio.

3. Baselines Clásicos

data_baselines.ipynb contiene:

- Análisis de los datasets
- Creación de baselines usados: Random, Most Popular, SVD, User and Item Mean.
- Evaluación de rating y ranking con métricas establecidas

# Datasets

recipes.csv contiene:
- RecipeId
- Name
- AuthorId
- AuthorName
- DatePublished
- Description
- Images
- RecipeCategory
- Keywords
- Ratings generales
- Ingredientes
- Instrucciones
- Calorías / macronutrientes

Se agrega el health score en cada notebook.

reviews.csv tiene:

- ReviewId
- RecipeId
- AuthorId 
- AuthorName 
- Rating
- Review
- DateSubmitted
- DateModified

# Licencia

Este proyecto es puramente académico.
No se incluyen claves API.
