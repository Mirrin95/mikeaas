# mikeaas
# Mikeaas - Mi Yo Digital (AI Clon) 🤖

Este repositorio contiene la estructura, la estrategia de dataset y la documentación para entrenar y desplegar a **Mikeaas**, un asistente virtual personalizado basado en modelos de lenguaje ajustados mediante **LoRA** (Low-Rank Adaptation).

## 🚀 Arquitectura del Proyecto
* **Modelo Base:** Llama-3-8B-Instruct (cuantizado a 4-bits)
* **Técnica de Entrenamiento:** QLoRA utilizando `Unsloth` en Google Colab con GPU T4.
* **Dataset:** Interacciones personalizadas basadas en estilo de comunicación, datos biográficos y redes sociales.
* **Modelo en la Nube:** Los adaptadores LoRA entrenados están alojados en Hugging Face: [`Mirrin95/mikeaas-lora`](https://huggingface.co/Mirrin95/mikeaas-lora).

## 📂 Estructura del Repositorio
* `dataset_example.json`: Formato de ejemplo utilizado para entrenar la personalidad.
* `train_mikeaas.ipynb`: Notebook con el paso a paso del código ejecutado en Colab.

## 🛠️ Cómo usarlo
Puedes cargar el modelo base y combinarlo con el LoRA directamente desde Hugging Face utilizando librerías como `transformers` y `peft`:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
from peft import PeftModel

base_model_id = "unsloth/llama-3-8b-Instruct-bnb-4bit"
model = AutoModelForCausalLM.from_pretrained(base_model_id, load_in_4bit=True)
tokenizer = AutoTokenizer.from_pretrained(base_model_id)

# Cargar tu LoRA desde Hugging Face
model = PeftModel.from_pretrained(model, "Mirrin95/mikeaas-lora")