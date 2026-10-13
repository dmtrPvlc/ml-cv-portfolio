#  ML & Computer Vision Portfolio
**Дмитрий Павлуцкий** | Senior ML Engineer / ML Pipeline Architect  
*Обезличенная демонстрация архитектуры ML-проектов, доведенных до production.*

---

##  Проект 1: Замкнутый цикл разметки и обучения (Smart Labeling Pipeline)
**Задача:** Ускорить подготовку датасетов для детекции объектов и повысить качество моделей за счет автоматизации.  
**Результат:** Скорость разметки выросла с 2 000 до 6 100 объектов/день (×2.5). Экономия ~2 FTE.

### Архитектура системы
```mermaid
graph TD
    A[Raw Video / Images] --> B(Извлечение кадров и предобработка)
    B --> C{Smart Annotator PyQt6}
    C -->|Auto-labeling| D[YOLO Ensemble + WBF]
    C -->|Refinement| E[SAM2 BBox Fitting]
    D --> F[(SQLite Metadata & Labels)]
    E --> F
    F --> G[Training Pipeline CLI/GUI]
    G -->|Multi-model: YOLO26s/m| H[TensorBoard & Metrics]
    H --> I[Plotly/HTML Analytics Report]
    I -->|Feedback Loop| C
    style C fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:2px
