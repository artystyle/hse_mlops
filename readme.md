# README.md

# MLOps Sandbox for HSE Students

Локальное окружение для работы с MLOps инструментами

## Сервисы

1. **Apache Airflow** 
   - URL: http://localhost:8080
   - Credentials: `airflow`/`airflow`

2. **JupyterLab**
   - URL: http://localhost:8888
   - Access token: `hse`

3. **MLflow Tracking**
   - URL: http://localhost:5000

4. **MinIO S3 Storage**
   - Console URL: http://localhost:9001
   - Credentials: `mlflow_access`/`mlflow_secret`

## Требования

- Docker 20.10+
- Docker Compose 2.0+

## Запуск

```bash
# Клонировать репозиторий (если требуется)
git clone https://github.com/hse-mlops/sandbox.git
cd sandboxПервоначальная настройка MinIO

    Откройте MinIO Console: http://localhost:9001

    Создайте bucket с именем mlflow

    Настройте доступ через IAM если требуется

Пример работы с MLflow и MinIO
```python
Copy

import mlflow

mlflow.set_tracking_uri("http://localhost:5000")
mlflow.set_experiment("hse-experiment")

with mlflow.start_run():
    mlflow.log_param("learning_rate", 0.01)
    mlflow.log_metric("accuracy", 0.95)
    mlflow.log_artifact("model.pkl", artifact_path="models")

Важные замечания

    Все данные сохраняются в Docker volumes

    Для доступа к MinIO из кода используйте:
    python
    Copy

    import os
    os.environ["AWS_ACCESS_KEY_ID"] = "mlflow_access"
    os.environ["AWS_SECRET_ACCESS_KEY"] = "mlflow_secret"
    os.environ["MLFLOW_S3_ENDPOINT_URL"] = "http://localhost:9000"

Copy


Это решение предоставляет:
- Изолированную среду для экспериментов с MLOps
- Интеграцию между MLflow и MinIO для артефактов
- Готовую среду для разработки моделей в Jupyter
- Оркестрацию пайплайнов через Airflow
- Сохранение данных между перезапусками контейнеров

Для использования в учебных целях рекомендуется:
1. Изучить документацию каждого инструмента
2. Экспериментировать с интеграцией компонентов
3. Модифицировать конфигурацию под конкретные задачи курса

# Запустить сервисы
docker-compose up -d

# Остановить сервисы
docker-compose down


Первоначальная настройка MinIO

    Откройте MinIO Console: http://localhost:9001

    Создайте bucket с именем mlflow

    Настройте доступ через IAM если требуется

Пример работы с MLflow и MinIO
python


import mlflow

mlflow.set_tracking_uri("http://localhost:5000")
mlflow.set_experiment("hse-experiment")

with mlflow.start_run():
    mlflow.log_param("learning_rate", 0.01)
    mlflow.log_metric("accuracy", 0.95)
    mlflow.log_artifact("model.pkl", artifact_path="models")

Важные замечания

    Все данные сохраняются в Docker volumes

    Для доступа к MinIO из кода используйте:
    python
    Copy

    import os
    os.environ["AWS_ACCESS_KEY_ID"] = "mlflow_access"
    os.environ["AWS_SECRET_ACCESS_KEY"] = "mlflow_secret"
    os.environ["MLFLOW_S3_ENDPOINT_URL"] = "http://localhost:9000"



Это решение предоставляет:
- Изолированную среду для экспериментов с MLOps
- Интеграцию между MLflow и MinIO для артефактов
- Готовую среду для разработки моделей в Jupyter
- Оркестрацию пайплайнов через Airflow
- Сохранение данных между перезапусками контейнеров

Для использования в учебных целях рекомендуется:
1. Изучить документацию каждого инструмента
2. Экспериментировать с интеграцией компонентов
3. Модифицировать конфигурацию под конкретные задачи курса

```