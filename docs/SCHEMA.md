# Esquema de Metadatos JSON (v2.1-ipfs)

## Introducción

Este documento describe la estructura y los campos del archivo principal de metadatos, `data/metadata.json`. Este archivo contiene un array (lista) de objetos JSON, donde cada objeto representa un único documento médico (tesis, paper, guía, etc.) archivado en el proyecto.

**Versión Actual del Esquema:** `2.1-ipfs`

## Estructura General

El archivo `metadata.json` es un array JSON:

```json
[
  { // Objeto representando el Documento 1
    "id": "...",
    "original_filename": "...",
    // ... otros campos ...
  },
  { // Objeto representando el Documento 2
    "id": "...",
    "original_filename": "...",
    // ... otros campos ...
  },
  // ... más documentos
]