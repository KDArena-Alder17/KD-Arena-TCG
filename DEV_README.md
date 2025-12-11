# Kloak 'n' Daggurr's – Developer Documentation

This document is intended for contributors or developers managing the Kloak 'n' Daggurr's trading card game repository. It explains the **folder structure, JSON/CSV workflows, Dulst integration, and asset management**.

---

## Folder Structure

KD-Arena-TCG/
├─ Decks/ # Local deck folders (optional to upload)
│ ├─ <Vigor Type>/ # Example: Chaos, Earth, etc.
│ │ ├─ <Deck Name>/ # Each deck folder
│ │ │ ├─ image.png # Card images
│ │ │ ├─ <Deck Name>.png # Deck QR code
│ │ │ └─ <Deck Name>.json # Original deck JSON
├─ CSV/ # Dulst-ready CSV exports
├─ JSON/ # Converted JSON files for Dulst
├─ scripts/ # Python scripts for conversion
├─ images/ # Optional: shared image repository
├─ README.md # Player-facing readme
└─ DEV_README.md # Developer documentation

yaml
Copy code

---

## Workflow Overview

1. **Deck JSON Conversion**  
   Use the `deck_converter.py` script to convert deck JSON files into the format required by Dulst. This creates:  
   - `deck_converted.json` → Normalized deck data  
   - `<Deck Name>_store.json` → Store metadata file

2. **CSV Export for Dulst**  
   Convert the normalized JSON into **Dulst-compatible CSV** files using the `json_to_csv.py` (or similar) script. Each row represents **one card** with the following columns:

| Column | Description |
|--------|-------------|
| deck_name | Name of the deck |
| card_name | Card's display name |
| vigor_type | One of the 14 Vigor Types |
| type | Card type: Creature, Primordial, Rune, Accoutrement, Vigor |
| rarity | Optional rarity field |
| filename | PNG image filename |
| image_url | GitHub Raw URL for the card image |

3. **Image Management**  
   - Multiple folders can be mirrored from your local machine to GitHub.  
   - Example: `Decks/Chaos/Chaotic Convergence/`  
   - GitHub Raw URLs will follow the path structure:  
     ```
     https://raw.githubusercontent.com/<username>/KD-Arena-TCG/main/Decks/Chaos/Chaotic Convergence/<filename>.png
     ```

4. **Adding New Decks**  
   - Create a new folder under the proper Vigor Type  
   - Place card images, QR code, and JSON  
   - Run the conversion scripts to update CSV files  
   - Commit and push to GitHub

---

## Scripts

- `deck_converter.py` → Converts master JSON into Dulst-ready JSON  
- `json_to_csv.py` → Converts JSON into CSV for Dulst import  
- `organize_decks.py` → Optional: Reorganizes folders and ensures images are consistent  

---

## Dulst Integration

1. Ensure CSV files are up to date and reference **GitHub Raw URLs** for images.  
2. Import CSV files into Dulst using the standard import tool.  
3. Test each deck to ensure images render and all card types appear correctly.  

---

## Contributor Guidelines

- Keep **folder names consistent** with Vigor Types  
- Use **lowercase or consistent capitalization** for filenames  
- Always regenerate CSV files after updating JSON  
- Include a commit message detailing which decks/cards were updated

---

## License

Refer to the `LICENSE` file in the repo for permitted usage and restrictions.
