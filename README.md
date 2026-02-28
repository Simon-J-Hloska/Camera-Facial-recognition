# Face Recognition System (Raspberry Pi)

## Přehled

Face Recognition System je Python aplikace pro rozpoznávání obličejů v reálném čase pomocí kamery Raspberry Pi.
Projekt umožňuje:

* sběr datasetu fotografií osob
* trénování modelu (face encodings)
* rozpoznávání osob ve video streamu

Aplikace využívá knihovny OpenCV, face_recognition a PiCamera2.

---

## Požadavky

* Python 3.9+
* Raspberry Pi (doporučeno Pi 4 nebo 5)
* Raspberry Pi Camera Module
* OS: Raspberry Pi OS (Bookworm nebo novější)

---

## Instalace

Nainstalujte závislosti:

```bash
pip install opencv-python face-recognition imutils numpy
```

Na Raspberry Pi může být nutné:

```bash
sudo apt install cmake libatlas-base-dev
```

---

## Struktura projektu

```
project/
│
├── dataset/                # Fotky osob
├── encodings.pickle        # Natrénované face encodings
├── capture_dataset.py      # Pořízení datasetu
├── train_model.py          # Trénování modelu
├── recognize.py            # Real-time rozpoznávání
```

---

## Konfigurace

Ve skriptu pro sběr dat změňte jméno osoby:

```python
PERSON_NAME = "Alfréd"
```

Toto jméno bude použito jako label pro rozpoznávání.

---

## 1️. Sběr datasetu

Spusťte skript pro focení datasetu:

```bash
python capture_dataset.py
```

Ovládání:

* **SPACE** → uloží fotku
* **Q** → ukončí focení

Fotky se ukládají do:

```
dataset/<person_name>/
```

---

## 2️. Trénování modelu

Vygeneruje encodings z datasetu:

```bash
python train_model.py
```

Výstup:

```
encodings.pickle
```

Tento soubor obsahuje:

* face embeddings
* jména osob

---

## 3️. Spuštění rozpoznávání

```bash
python recognize.py
```

Funkce:

* detekce obličejů v reálném čase
* porovnání s databází
* vykreslení jména nad obličejem
* zobrazení FPS

Ukončení:
Stiskněte **Q**

---

## Jak to funguje

### Pipeline

1. Capture obrázků osob
2. Extrakce face encodings
3. Serializace do pickle
4. Real-time matching

---

## Použité technologie

* Python
* OpenCV
* face_recognition (dlib)
* PiCamera2
* NumPy

---

## Optimalizace výkonu

Projekt používá:

* downscaling framů (`cv_scaler`)
* batch encoding
