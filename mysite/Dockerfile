FROM python:3.8-slim-buster

# Python environment setup
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Create and set working directory
ENV PROJECT=/home/app

RUN mkdir -p ${PROJECT}
RUN mkdir -p ${PROJECT}/static
WORKDIR ${PROJECT}

# Packages required for setting up WSGI
RUN apt-get update
RUN apt-get install -y --no-install-recommends gcc libc-dev python3-dev

# Copy and install requirements
RUN pip install --upgrade pip
COPY ./requirements.txt ${PROJECT}/requirements.txt
RUN pip install -r ${PROJECT}/requirements.txt
RUN pip install django-prometheus

# Copy project to working directory
COPY . ${PROJECT}

RUN python3 manage.py migrate

EXPOSE 8000

CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "mysite.wsgi:application"]


