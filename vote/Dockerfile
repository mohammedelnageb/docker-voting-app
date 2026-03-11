FROM python:3.11-slim

WORKDIR /app

#COPY requirements.txt .
RUN pip install gunicorn flask Redis

COPY . .

EXPOSE 80

CMD ["gunicorn", "--bind", "0.0.0.0:80", "--access-logfile", "-", "app:app"]
