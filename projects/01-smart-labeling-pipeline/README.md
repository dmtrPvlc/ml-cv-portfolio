# Проект 1: Замкнутый цикл Smart Labeling и Training Pipeline

## Описание задачи

Ускорить подготовку датасетов для детекции объектов и повысить качество итоговых моделей за счет минимизации ручного труда и внедрения строгого контроля качества данных на этапе разметки.

## Решение

Разработана единая экосистема из 4-х связанных модулей: база данных с метаданными, полуавтоматический аннотатор с AI-подсказками, CLI/GUI training pipeline и система аналитической отчетности для диагностики проблем обучения.

## Результаты и метрики

- Скорость разметки: рост с 2 000–2 500 до 6 100 объектов в день (x2.5).
- Доля автоматизации: ~70% авторазметки, ~30% ручной коррекции.
- Экономический эффект: эквивалент экономии 2 FTE (полных ставок) разметчиков.
- Качество моделей: mAP50 = 0.80, mAP50-95 = 0.63, Precision = 0.91, Recall = 0.76 (YOLO26s, 896px).
- Рост метрик: улучшение показателей обучения на ~10% за счет внедрения эвристической и AI-валидации датасета перед обучением.
- Инференс: 72–143 FPS в зависимости от разрешения и модели.

## Технологический стек

- Python
- PyQt6 (thread-safe архитектура, QThread, сигналы)
- Ultralytics (YOLOv8/v11/v26, SAM2)
- Ensemble Boxes (Weighted Boxes Fusion)
- SQLite3
- Streamlit
- Plotly, Matplotlib
- TensorBoard
- psutil, GPUtil
- Форматы: YOLO, COCO, Pascal VOC, SuperAnnotate, JSON, CSV, XML
- Git (локальный репозиторий)

## Архитектура системы

```mermaid
graph TD
    A[Raw Video / Images] --> B[Предобработка и извлечение кадров]
    B --> C{Smart Annotator PyQt6}
    C -->|Auto-labeling| D[YOLO Ensemble + WBF]
    C -->|Refinement| E[SAM2 BBox Fitting]
    D --> F[(SQLite: Metadata & Labels)]
    E --> F
    F --> G[Training Pipeline CLI/GUI]
    G -->|Multi-model: YOLO26s/m| H[TensorBoard & Metrics]
    H --> I[Plotly/HTML Analytics Report]
    I -->|Feedback Loop| C
