# layout-quality-analyzer

[![Python](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/github/license/user/repo)](LICENSE)

## Описание

Проект по автоматической классификации HTML-макетов на "хорошие" и "плохие" с использованием **Random Forest** и **анализа HTML-контента**.

## Метрики

| Модель             | Accuracy | F1-score | ROC-AUC |
|--------------------|----------|----------|---------|
| Random Forest      | 0.97     | 0.97     | 0.99    |
| Gradient Boosting  | 0.97     | 0.97     | 1.00    |

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

## Установка и запуск

### С виртуальным окружением:

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# или
venv\Scripts\activate     # Windows
pip install -r requirements.txt
python main.py

docker build -t layout-analyzer .
docker run layout-analyzer
