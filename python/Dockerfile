FROM lambci/lambda:build-python3.7

COPY ./manage.py /var/task
COPY ./requirements.txt /var/task

RUN pip install --no-cache-dir -U pip -r requirements.txt
