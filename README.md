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
layout-quality-analyzer/ │ ├── src/ │ ├── init.py │ ├── model.py │ ├── data_loader.py │ └── train.py │ ├── data/ │ └── sample_data.csv │ ├── requirements.txt ├── main.py ├── Dockerfile ├── README.md └── .gitignore

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
