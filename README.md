# 🚘 PlateVision AI

<div align="center">

### Automatic Number Plate Recognition using YOLOv9, DeepSORT & OCR

**An end-to-end computer vision pipeline for vehicle detection, tracking, classification, licence plate detection and character recognition.**

[![ResearchGate](https://img.shields.io/badge/ResearchGate-Read_the_Research-00CCBB?style=for-the-badge&logo=researchgate&logoColor=white)](https://www.researchgate.net/publication/393557998_Synergetic_Integration_of_YOLOv9_DeepSORT_and_PaddleOCR_Revolutionizing_ANPR_Technology)
[![DOI](https://img.shields.io/badge/Springer-10.1007%2F978--981--96--3361--6__15-013243?style=for-the-badge&logo=springer&logoColor=white)](https://doi.org/10.1007/978-981-96-3361-6_15)
![YOLOv9](https://img.shields.io/badge/YOLO-v9-blue?style=flat-square)
![DeepSORT](https://img.shields.io/badge/Tracking-DeepSORT-orange?style=flat-square)
![OCR](https://img.shields.io/badge/OCR-PaddleOCR-green?style=flat-square)

</div>

---

## 🏆 Published Results

> ### 📊 YOLOv9 Licence Plate Detection
>
> | Metric | Result |
> |:--|--:|
> | **mAP@50** | **98.6%** |
> | **Precision** | **98.3%** |
> | **Recall** | **95.8%** |
> | **mAP@50–95** | **72.7%** |
>
> ### 🔤 End-to-End ANPR Performance
>
> | Evaluation | Result |
> |:--|--:|
> | **Correctly detected plate characters — final output** | **97.47%** |
> | **Correctly detected characters across frames** | **92.15%** |
> | **Correctly recognised licence plates — final output** | **82.35%** |

> [!IMPORTANT]
> These results are reported in the associated peer-reviewed research publication:  
> **“Synergetic Integration of YOLOv9, DeepSORT, and PaddleOCR: Revolutionizing ANPR Technology.”**

### 🔬 [View the research on ResearchGate →](https://www.researchgate.net/publication/393557998_Synergetic_Integration_of_YOLOv9_DeepSORT_and_PaddleOCR_Revolutionizing_ANPR_Technology)

---

## 📖 About PlateVision AI

**PlateVision AI** is an Automatic Number Plate Recognition (ANPR) system designed to detect vehicles, maintain their identities across video frames, locate their licence plates and recognise the characters on those plates.

Rather than treating ANPR as a single detection problem, the project combines multiple computer-vision stages into one pipeline:

**Vehicle Detection → Vehicle Classification → Multi-Object Tracking → Licence Plate Detection → Image Preprocessing → OCR → Vehicle/Plate Association**

The repository originated with YOLOv9, DeepSORT and EasyOCR experimentation. The associated published research extends the recognition pipeline using **PaddleOCR**.

---

## ⚙️ Architecture

```text
                        INPUT VIDEO
                             │
                             ▼
                  ┌─────────────────────┐
                  │       YOLOv9        │
                  │  Vehicle Detection  │
                  └──────────┬──────────┘
                             │
                 Vehicle Class (COCO)
                             │
                             ▼
                  ┌─────────────────────┐
                  │      DeepSORT       │
                  │ Multi-Object Track  │
                  │ Persistent IDs      │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │       YOLOv9        │
                  │ Custom Plate Model  │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │ Plate Preprocessing │
                  │ Grayscale / Denoise │
                  │ Threshold / Filter  │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │     PaddleOCR       │
                  │ Character Reading   │
                  └──────────┬──────────┘
                             │
                             ▼
                   VEHICLE + PLATE OUTPUT
```

---

## ✨ Key Features

### 🎯 YOLOv9 Object Detection
YOLOv9 is used for object detection within the ANPR pipeline. Vehicles are detected from video frames, while a custom-trained model is used for licence plate localisation.

### 🧠 Train Your Own YOLOv9 Model
The project supports custom YOLOv9 training for licence plate detection rather than relying only on generic pre-trained object classes.

### 🚗 DeepSORT Vehicle Tracking
**DeepSORT** tracks detected vehicles throughout a video and assigns persistent IDs. This makes it possible to associate a plate with the same vehicle across multiple frames instead of treating each frame independently.

### 🚙 Vehicle Type Identification
COCO object classes are used to identify relevant moving vehicle types and combine vehicle classification with the tracking pipeline.

### 🔤 OCR Recognition
Detected licence-plate regions are extracted and processed before OCR. Early repository development used **EasyOCR**, while the published research pipeline integrates **PaddleOCR**.

---

## 📦 Research Dataset & Training

The custom licence-plate detector used in the research was trained using transfer learning.

| Property | Research Setup |
|:--|--:|
| **Dataset size** | **10,126 images** |
| **Training split** | **70%** |
| **Validation split** | **20%** |
| **Test split** | **10%** |
| **Training duration** | **100 epochs** |

The dataset includes licence plates with variation in **size, shape, colour, viewing angle and background**, helping the detector generalise across different road scenes.

---

## 🔬 Research

This project is associated with the peer-reviewed publication:

> **Synergetic Integration of YOLOv9, DeepSORT, and PaddleOCR: Revolutionizing ANPR Technology**  
> **Abheek Kaushal, Archisha Singh, Ankita Roy & Manoj Kumar**  
> *Proceedings of Data Analytics and Management — ICDAM 2024, Volume 4*  
> Springer Nature Singapore, 2025 · pp. 189–197

### Research Links

🔬 **[ResearchGate — View Publication](https://www.researchgate.net/publication/393557998_Synergetic_Integration_of_YOLOv9_DeepSORT_and_PaddleOCR_Revolutionizing_ANPR_Technology)**

📚 **[Springer DOI — 10.1007/978-981-96-3361-6_15](https://doi.org/10.1007/978-981-96-3361-6_15)**

---

## 🛠️ Technology Stack

| Area | Technology |
|:--|:--|
| Object Detection | **YOLOv9** |
| Multi-Object Tracking | **DeepSORT** |
| OCR | **PaddleOCR / EasyOCR experimentation** |
| Vehicle Classification | **COCO Dataset Classes** |
| Image & Video Processing | **OpenCV** |
| Language | **Python** |
| Model Training | **Google Colab Pro** |

---

## 🧪 Pipeline Output

For each tracked vehicle, the pipeline can associate information such as:

```text
Vehicle Track ID
Vehicle Type
Vehicle Bounding Box
Licence Plate Bounding Box
Licence Plate Number
Detection / Recognition Confidence
```

Tracking across frames provides multiple opportunities to detect and recognise the same plate, improving the robustness of the final vehicle-to-plate association.

---

## 📝 Citation

If this repository or the associated research contributes to your work, please cite:

```bibtex
@incollection{kaushal2025anpr,
  title     = {Synergetic Integration of YOLOv9, DeepSORT, and PaddleOCR:
               Revolutionizing ANPR Technology},
  author    = {Kaushal, Abheek and Singh, Archisha and Roy, Ankita and Kumar, Manoj},
  booktitle = {Proceedings of Data Analytics and Management},
  pages     = {189--197},
  year      = {2025},
  publisher = {Springer Nature Singapore},
  doi       = {10.1007/978-981-96-3361-6_15}
}
```

---

## 👨‍💻 Author

### Abheek Kaushal

Computer Vision · Artificial Intelligence · Deep Learning

[![ResearchGate](https://img.shields.io/badge/ResearchGate-Research-00CCBB?style=for-the-badge&logo=researchgate&logoColor=white)](https://www.researchgate.net/publication/393557998_Synergetic_Integration_of_YOLOv9_DeepSORT_and_PaddleOCR_Revolutionizing_ANPR_Technology)
[![GitHub](https://img.shields.io/badge/GitHub-AbheekKaushal-181717?style=for-the-badge&logo=github)](https://github.com/AbheekKaushal)

---

<div align="center">

**YOLOv9 × DeepSORT × PaddleOCR**

If you find **PlateVision AI** useful, consider giving the repository a ⭐.

</div>
