# FROM python:3.13-slim - has no git, needed for the current requirements.txt
FROM python:3.13

COPY requirements.txt /app/
WORKDIR /app
RUN python -m pip install -r requirements.txt

COPY main.py /app

ENTRYPOINT ["python", "main.py"]
