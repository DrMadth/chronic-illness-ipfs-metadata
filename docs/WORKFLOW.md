# Workflow para Añadir Nuevos Documentos (IPFS)

## Objetivo

Este documento describe el proceso paso a paso para añadir un nuevo documento médico (PDF) al archivo descentralizado IPFS y registrar sus metadatos correspondientes en el archivo `data/metadata.json`. Seguir estos pasos asegura la consistencia y la persistencia de la información.

## Prerrequisitos

* **Software IPFS Instalado:** Necesitas tener una implementación de IPFS instalada y funcionando en tu máquina local. Se recomienda [Kubo (go-ipfs)](https://docs.ipfs.tech/install/command-line/). Debes poder ejecutar el demonio IPFS (`ipfs daemon`).
* **Acceso a Servicio de Pinning (Recomendado):** Una cuenta (puede ser gratuita) en un servicio de pinning de IPFS como [Pinata Cloud](https://pinata.cloud/), [Web3.Storage](https://web3.storage/), [Filebase](https://filebase.com/), Infura, etc. Esto es **esencial** para asegurar que el archivo persista online.
* **Editor de Texto / JSON:** Un editor que maneje bien archivos JSON (como VS Code, Notepad++, Sublime Text) para editar `metadata.json` sin errores de sintaxis.
* **(Opcional pero Recomendado) Git:** Si se usa control de versiones, tener Git instalado.

## Pasos Detallados

1.  **Obtener el Documento PDF:**
    * Descarga o consigue el archivo PDF del documento que quieres añadir.
    * Verifica que sea la versión correcta y, si es posible, que sea legible y accesible (preferiblemente Open Access).
    * Guarda el PDF en una ubicación temporal en tu disco local (puedes usar una carpeta como `data/pdfs_a_procesar/` si la creaste).

2.  **Verificar Duplicados (Recomendado):**
    * **Revisa `data/metadata.json`:** Busca por título o DOI para asegurarte de que este documento no ha sido añadido previamente.
    * **(Avanzado):** Busca en archivos públicos de IPFS (como Anna's Archive) si este PDF exacto ya existe y tiene un CID conocido. Si lo encuentras y verificas que es el mismo archivo, puedes usar ese CID existente en el Paso 4 y saltarte el Paso 3.

3.  **Añadir el PDF a tu Nodo IPFS Local:**
    * **Inicia tu demonio IPFS:** Abre una terminal y ejecuta `ipfs daemon`. Déjala corriendo en segundo plano.
    * **Añade el archivo:** Abre *otra* terminal, navega a la carpeta donde tienes el PDF y ejecuta:
      ```bash
      # Reemplaza /ruta/completa/al/documento.pdf con la ruta real
      ipfs add "/ruta/completa/al/documento.pdf" --cid-version 1 
      ```
      * La opción `--cid-version 1` asegura que obtengas un CID en formato `bafy...` (más compatible con gateways web).
    * **Copia el CID:** El comando devolverá una línea similar a `added <CID> documento.pdf`. Copia cuidadosamente el **CID** (la cadena larga que empieza por `bafy...`). Este es el identificador único de tu archivo en IPFS.

4.  **Asegurar Persistencia (Pinning - ¡¡CRÍTICO!!):**
    * Subir el archivo a tu nodo local (paso 3) no es suficiente para que esté siempre disponible. Debes "fijarlo" (pin).
    * **a) Pin Local:** En la terminal, ejecuta:
        ```bash
        ipfs pin add <EL_CID_QUE_OBTUVISTE> 
        ```
        Esto asegura que *tu* nodo no borre el archivo, pero solo estará disponible mientras tu nodo esté encendido.
    * **b) Pin Remoto (ESENCIAL):** Elige **al menos una** de estas opciones:
        * **Usar un Servicio de Pinning:** Esta es la forma más sencilla y fiable de empezar.
            * Ve a la web del servicio que hayas elegido (ej. Pinata, Web3.Storage).
            * Sigue sus instrucciones para subir el archivo PDF original O (más eficientemente) para hacer "pin" usando el **CID** que obtuviste en el paso 3.
            * Verifica en el panel del servicio que el CID aparece como "pineado" (pinned).
            * *[Aquí se podrían añadir instrucciones más detalladas para el servicio específico elegido por la comunidad, ej: "Instrucciones para Pinata: Ir a 'Pin Manager' -> 'Pin By CID' -> Pegar el CID y dar un nombre"]*
        * **Nodos Comunitarios:** Si otros miembros de confianza de la comunidad tienen nodos IPFS activos, pídeles que también ejecuten `ipfs pin add <EL_CID_QUE_OBTUVISTE>` en sus nodos. Cuantos más nodos lo tengan pineado, más robusto y descentralizado será el acceso.

5.  **Recopilar Metadatos del Documento:**
    * Reúne toda la información necesaria para completar la entrada en `metadata.json`, siguiendo la estructura definida en `docs/SCHEMA.md`.
    * Campos clave: `title`, `authors` (con nombre, opcionalmente afiliación/orcid), `publication_date`, `language`, `document_type`, `is_open_access`, `clinical_conditions` (con `ontology`, `code`, `term` y `short_code`), `keywords`, `abstract_summary` (corto), `document_text_extract` (abstract completo o texto extenso), `source_details` (info de revista o tesis, incluyendo DOI si aplica), `metadata_version` (ej. `"2.1-ipfs"`), `ipfs_gateways` (opcional).

6.  **Editar y Validar `data/metadata.json`:**
    * Abre el archivo `data/metadata.json` con un editor de texto que entienda JSON (recomendado VS Code con alguna extensión de validación JSON).
    * **Navega hasta el final del array** (justo antes del `]` final).
    * **Añade una coma (`,`)** después del último objeto `}` existente (si no es el primer documento que añades).
    * **Pega un nuevo objeto `{}`** y rellena todos los campos que recopilaste en el paso 5. Asegúrate de usar comillas dobles `"` para todas las claves y los valores de texto.
    * **¡IMPORTANTE!** En el campo `"id"`, pon el **CID IPFS** que obtuviste en el Paso 3.
    * **Valida la Sintaxis JSON:** Antes de guardar, asegúrate de que la sintaxis JSON es correcta. Un error (una coma de más o de menos, una comilla olvidada) hará que el archivo sea inválido. Usa el validador de tu editor o un validador online si tienes dudas.
    * **Guarda** el archivo `metadata.json`.

7.  **Control de Versiones (Si usas Git/GitHub):**
    * Abre tu terminal en la carpeta raíz del proyecto (`D:\DCNDB`).
    * Añade el archivo modificado al "staging area" de Git:
      ```bash
      git add data/metadata.json 
      ```
    * Crea un "commit" (una foto del cambio) con un mensaje descriptivo:
      ```bash
      git commit -m "Add metadata for CID: [primeros 7 caracteres del CID]" 
      ```
      *(Reemplaza `[primeros...CID]` por el inicio del CID real)*.
    * Sube los cambios al repositorio remoto (ej. GitHub):
      ```bash
      git push origin main 
      ```
      *(O el nombre de tu rama principal)*.

8.  **Limpieza Local (Opcional):**
    * Si guardaste el PDF original en una carpeta temporal como `data/pdfs_a_procesar/`, puedes moverlo a `data/pdfs_procesados/` para saber que ya está gestionado.

---