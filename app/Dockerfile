FROM python:3.12-bookworm
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install postgresql-client

WORKDIR /server

COPY ./pyproject.toml .
RUN pip install --upgrade pip && pip install poetry
RUN poetry config virtualenvs.create false && poetry install --no-dev
RUN poetry add gunicorn

CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:8000", "run:app"]