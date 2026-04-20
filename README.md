# Lab 4: Identity Preservation & Advanced Workflows en ComfyUI

Este repositorio documenta el desarrollo y la experimentación con flujos de trabajo avanzados en **ComfyUI**, utilizando la arquitectura de **Stable Diffusion 1.5** para la transformación de retratos reales en escenas cinematográficas y épicas.

##  Objetivo General
El proyecto se centra en dominar técnicas de **Identity Preservation** (Preservación de Identidad) para situar a sujetos reales en entornos generados sintéticamente, garantizando la coherencia visual y biométrica.

##  Tecnologías y Modelos
* **Plataforma:** ComfyUI.
* **Modelos Base:** `Stable Diffusion v1.5` y `DreamShaper 8`.
* **Control de Identidad:** `IP-Adapter Plus` (Preset: PLUS FACE) con codificación `ViT-H-14`.
* **Control Estructural:** `OpenPose` (ControlNet) para la gestión de anatomía en escenas grupales.
* **Refinamiento:** Escalado latente (Hires. Fix) para la mejora de micro-texturas y rasgos faciales.

---

##  Niveles de Implementación y Resultados

| Nivel | Tipo de Cambio | Logro Principal | Técnica Clave |
| :--- | :--- | :--- | :--- |
| **1** | Leve (Img2Img) | Retratos corporativos profesionales desde fotos casuales. | `Denoise` bajo (0.2 - 0.4) para conservar estructura. |
| **2** | Moderado (Txt2Img) | Recontextualización en laboratorios futuristas. | Generación desde latente vacío (alucinación de fondo). |
| **3** | Fuerte (Escena Grupal) | Escena épica medieval unificada con tres integrantes. | Máscaras Regionales + Daisy Chaining de IP-Adapters. |

### Detalles Técnicos por Nivel

#### 1. Nivel 1: Edición Profesional
Se enfocó en la preservación total de la imagen original. Un valor de **denoise entre 0.2 y 0.4** permitió que la IA inyectara texturas de iluminación de estudio sin alterar la fisionomía del usuario.

#### 2. Nivel 2: Generación Sintética
Se evidenció que para reconstruir fondos complejos (como laboratorios), el flujo Img2Img era insuficiente. Se migró a **generación desde espacio latente vacío**, permitiendo que el checkpoint "alucinara" el entorno mientras el IP-Adapter anclaba la identidad.

#### 3. Nivel 3: Composición Multisujeto
Implementación de una arquitectura en cascada para gestionar múltiples identidades. Se superaron los problemas de **clonación de rostros** mediante el uso de esqueletos de pose de **ControlNet**, obligando a la IA a asignar una identidad distinta a cada esqueleto detectado.

---

## Limitaciones y Desafíos
* **Resolución Inicial:** SD 1.5 presenta dificultades para renderizar rasgos en planos generales (caras pequeñas). Esto se mitigó con procesos de **segunda pasada** y escalado latente.
* **Clonación de Sujetos:** La tendencia natural del modelo a repetir la misma identidad en escenas grupales fue el obstáculo más crítico, resuelto con control de pose externo.
* **Prueba y Error:** La alineación de máscaras regionales y la calibración de pesos de atención (`weights`) requiere una intervención manual precisa; no es un proceso automatizado de un solo clic.

## Conclusiones
Los resultados demuestran que, a través de un ejercicio de **refinamiento iterativo** y el uso estratégico de máscaras, es posible generar escenas grupales complejas con alta fidelidad. Este laboratorio valida que el ecosistema de adaptadores modulares permite el desarrollo de proyectos de **identidad digital de alta calidad** con un control granular sobre la composición final.
