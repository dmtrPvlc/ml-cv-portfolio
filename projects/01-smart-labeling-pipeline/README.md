#  Проект 1: Замкнутый цикл Smart Labeling и Training Pipeline

##  Бизнес-задача
Ускорить подготовку датасетов для детекции объектов и повысить качество итоговых моделей за счет минимизации ручного труда и внедрения контроля качества данных на этапе разметки.

##  Решение
Разработана единая экосистема из 4-х связанных модулей: база данных с метаданными, полуавтоматический аннотатор с AI-подсказками, CLI/GUI training pipeline и система аналитической отчетности.

##  Архитектура системы
```mermaid
graph TD
    A[Raw Video / Images] --> B(Предобработка и извлечение кадров)
    B --> C{Smart Annotator PyQt6}
    C -->|Auto-labeling| D[YOLO Ensemble + Weighted Boxes Fusion]
    C -->|Refinement| E[SAM2 BBox Fitting]
    D --> F[(SQLite: Metadata & Labels)]
    E --> F
    F --> G[Training Pipeline CLI/GUI]
    G -->|Multi-model: YOLOv8/v11| H[TensorBoard & Metrics]
    H --> I[Plotly/HTML Analytics Report]
    I -->|Feedback Loop: авто-рекомендации| C
    
    style C fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:2px
    style F fill:#ff9,stroke:#333,stroke-width:2px
