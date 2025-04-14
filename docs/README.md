# Decentralized Chronic Neurological Conditions Document Archive (Librarian DCN)

## Overview

This project aims to create and maintain a **decentralized**, **collaborative**, and **censorship-resistant** archive of relevant medical documents (PhD theses, scientific papers, clinical guidelines, reports, etc.) focusing on conditions such as **Myalgic Encephalomyelitis / Chronic Fatigue Syndrome (ME/CFS)**, **Dysautonomia** (including POTS), **Post-COVID Syndrome (Long Covid)**, and frequently associated conditions (e.g., Ehlers-Danlos Syndromes - EDS).

The goal is to provide a reliable and accessible resource for patients, caregivers, researchers, and medical professionals, curated and managed by the community itself using IPFS for storage.

**Current Status:** In Development - Defining data structure (`metadata.json`), documentation, and contribution workflow.

## Project Context: Decentralized Chronic Network (DCN)

This document archive is a foundational component of the broader **Decentralized Chronic Network (DCN)** initiative.

The overall mission of DCN is to empower patients with chronic conditions through community-governed, decentralized tools and data resources. We aim to leverage collective knowledge, data aggregation (including future integration of biomarker and device data), and potentially AI tools to accelerate understanding, improve quality of life, and advocate for better research and care, free from centralized control or censorship.

Future related projects within DCN may include a decentralized digital identity system for governance and secure data sharing.

*For more details on the vision, foundational principles, and governance ideas for DCN, please see `docs/VISION.md` (to be created).*

## Key Technologies

* **Database:** JSON (`data/metadata.json`)
* **File Storage:** IPFS (InterPlanetary File System)
* **Version Control (Recommended):** Git / GitHub
* **Future (Optional):** Telegram Bot Interface, Python scripts for management, potential deployment on Cloud Run using Docker.

## Folder Structure (Proposed)
```
/ (Project Root - D:\DCNDB)
|-- data/              # Contains metadata.json and temporary PDFs
|   |-- metadata.json
|-- docs/              # Project documentation
|   |-- README.md      (This file)
|   |-- SCHEMA.md      (Detailed JSON schema description)
|   |-- WORKFLOW.md    (Steps for adding new documents)
|   |-- VISION.md      (Overall DCN vision - Optional, To be created)
|-- src/               # (Optional) Future source code for bot/scripts
|-- .gitignore         # Files ignored by Git (IMPORTANT!)
```

## How to Use or Contribute

1.  **Explore Data:** Review the `data/metadata.json` file to see indexed documents. Use the `id` field (which is the IPFS CID) to access the corresponding PDF file via a public IPFS gateway (see `ipfs_gateways` list within the JSON) or your own local IPFS node. Example Link: `https://ipfs.io/ipfs/YOUR_CID_HERE`.
2.  **Understand the Schema:** Consult `docs/SCHEMA.md` for a detailed description of each field in `metadata.json`.
3.  **Add New Documents:** Collaboration is welcome! Please rigorously follow the steps outlined in `docs/WORKFLOW.md`. This requires basic knowledge of IPFS (installing a local node, adding files, getting CIDs) and access to a pinning service or the willingness to run a persistent node.
4.  **Version Control:** Using Git and platforms like GitHub is recommended for proposing changes or adding new entries to `metadata.json` in an orderly fashion via Pull Requests (if a repository is set up).

## Contact / Maintainer

* **Email:** Airmid4ME@proton.me
* **X (Twitter):** @DChronicNet
* *(Consider adding other relevant public contact methods if desired)*

## Community & Other Ways to Help

You don't need to be an IPFS expert to contribute to this project! Your insights, document findings, and feedback are highly valuable to the DCN community.

* **Suggest Documents:** If you find relevant papers, theses, guidelines, or other documents that you think should be included in the archive, but you are not familiar with the IPFS workflow, please let us know! You can send us the details (Title, Author, Year, Link/DOI or the PDF file itself) via Email or X (Twitter). The maintainers will review it and add it to the archive if appropriate, following the defined [Workflow](WORKFLOW.md).
* **Provide Feedback:** As we develop tools to interact with this data (like the future Telegram bot), we will need feedback from the community (patients, caregivers, researchers) to make them truly useful. Your ideas, bug reports, and suggestions on usability are welcome through our contact channels.
* **Spread the Word:** Help make this resource known within the relevant patient and research communities (ME/CFS, Dysautonomia, Long Covid, EDS, etc.).

**Get in touch or send suggestions via:**
* **Email:** Airmid4ME@proton.me
* **X (Twitter):** @DChronicNet

---
*Last Updated: April 14, 2025*