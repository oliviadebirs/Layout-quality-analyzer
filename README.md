# Layout Quality Analyzer

[![Python](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/github/license/user/repo)](LICENSE)

## Описание

Проект по автоматической классификации HTML-макетов (например, веб-страниц, презентаций, email-шаблонов) на **"хорошие"** и **"плохие"**.  
Анализ производится на основе **HTML-кода макета** с извлечением **структурных, текстовых и стилевых признаков**.  
Для классификации используется **Random Forest** и другие модели машинного обучения.

## Метрики

| Модель             | Accuracy | F1-score | ROC-AUC |
|--------------------|----------|----------|---------|
| Random Forest      | 0.97     | 0.97     | 0.99    |
| Gradient Boosting  | 0.97     | 0.97     | 1.00    |

**Примечание:** Высокие метрики обусловлены информативностью признаков и небольшим, но чётко разделённым датасетом.

## Основные признаки

Модель использует признаки, извлечённые из HTML-кода:

- `link_count`: Количество ссылок `<a>` на странице.
- `width_min`: Минимальная ширина элементов (px).
- `total_text_length`: Общее количество символов текста.
- `font-size_mean`: Средний размер шрифта (px).
- `rotate_mean`: Средний угол поворота элементов (deg).
- `height_mean`: Средняя высота элементов (px).
- и другие (см. `src/data_loader.py`).

## Структура проекта
layout-quality-analyzer/
│
├── data/
│   ├── raw/
│   │   ├── good.json
│   │   └── bad.json
│   └── processed/
│       └── features.csv          # После извлечения признаков
│
├── src/
│   ├── __init__.py
│   ├── data_loader.py            # Загрузка JSON, декодирование HTML
│   ├── feature_extractor.py      # Извлечение признаков из HTML
│   ├── preprocessing.py          # Очистка, удаление корреляций, стандартизация
│   ├── model.py                  # Определение моделей
│   ├── train.py                  # Обучение, оценка, кросс-валидация
│   ├── evaluation.py             # Сравнение метрик, важность признаков
│   └── visualization.py          # Визуализация: корреляции, важность, боксплоты
│
├── notebooks/
│   └── exploratory_analysis.ipynb # Для анализа, визуализации, экспериментов
│
├── tests/                        # (опционально)
│   └── test_features.py
│
├── requirements.txt
├── main.py                       # Запуск основного пайплайна
├── README.md
├── .gitignore
├── Dockerfile
└── .dockerignore                

## Данные
Данные представлены в формате JSON, где каждый элемент содержит ключ content с HTML-кодом макета.

good.json: содержит HTML-код «хороших» макетов.
bad.json: содержит HTML-код «плохих» макетов.

## Обработка и обучение
Декодирование HTML-сущностей.
Извлечение признаков:
Структурные (количество тегов, количество ссылок).
Стилистические (размеры шрифтов, ширина/высота, повороты).
Текстовые (объём текста).
Удаление дубликатов и коррелирующих признаков.
Обучение и оценка моделей RandomForest, GradientBoosting, LogisticRegression, KNN.
Кросс-валидация для оценки стабильности.

## Презентации
Хорошие макеты
Плохие макеты 
Ссылки будут предоставлены по запросу. 

## Установка и запуск

### С виртуальным окружением:

```bash
git clone https://github.com/oliviadebirs/layout-quality-analyzer.git
cd layout-quality-analyzer

python -m venv venv
source venv/bin/activate  # Linux/Mac
# или
venv\Scripts\activate     # Windows

pip install -r requirements.txt
python main.py

git clone https://github.com/oliviadebirs/layout-quality-analyzer.git
cd layout-quality-analyzer

docker build -t layout-analyzer .
docker run layout-analyzer
