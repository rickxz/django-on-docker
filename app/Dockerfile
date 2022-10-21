# pull official base image
FROM python:3.9.6-alpine

# set work directory
# workdir on windows: https://learn.microsoft.com/pt-br/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile
WORKDIR /python-scripts/django-on-docker/app

# set environmental variables
# pythondontwritebytecode: prevents python from writing pyc files to disc
# pythonnunbuffered: prevents python from buffering stdout and stderr (equivalent to python -u)
ENV PYTHONDONTWRITEBYTECODE 1 
ENV PYTHONNUNBUFFERED 1

# install psycopg2 dependencies
RUN apk update \
    && apk add postgresql-dev gcc python3-dev musl-dev

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# copy entrypoint.sh
COPY ./entrypoint.sh .
RUN sed -i 's/\r$//g' /python-scripts/django-on-docker/app/entrypoint.sh
RUN chmod +x /python-scripts/django-on-docker/app/entrypoint.sh

# copy project
COPY . .

# run entrypoint.sh
ENTRYPOINT ["/python-scripts/django-on-docker/app/entrypoint.sh"]