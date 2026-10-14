
---

#### 4. Проект 2: `projects/02-ocr-vlm-arbitration/README.md`

```markdown
#  Проект 2: Интеллектуальная обработка документов (OCR + VLM)

##  Бизнес-задача
Автоматизировать извлечение структурированных данных (таблицы, текст) из сложных PDF-документов с высокой точностью, минимизируя ошибки классических OCR-систем.

##  Решение
Создан гибридный конвейер: классические быстрые OCR-движки используются для массовой обработки, а легковесная локальная Vision-Language Model (VLM) подключается только для семантического арбитража спорных или нечетких участков текста.

##  Архитектура конвейера
```mermaid
graph LR
    A[Input PDF] --> B(pypdfium2: Извлечение страниц)
    B --> C{Классификация блока}
    C -->|Текст| D[Surya OCR / Tesseract]
    C -->|Таблицы| E[OpenCV / Эвристики]
    D --> F[LLM Arbitration Layer]
    E --> F
    F -->|Qwen2.5-VL Prompting| G[(Structured Excel/JSON)]
    
    style F fill:#ff9,stroke:#333,stroke-width:2px
    style G fill:#9f9,stroke:#333,stroke-width:2px
