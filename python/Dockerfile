FROM python:3.13-slim

COPY requirements.txt /app/
WORKDIR /app
RUN python -m pip install -r requirements.txt

COPY main.py /app

ENTRYPOINT ["python", "main.py"]
