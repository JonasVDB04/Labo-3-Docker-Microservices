FROM python:3.13.2-alpine3.21 AS build-image

WORKDIR '/app'

RUN apk add --no-cache linux-headers g++

COPY ./requirements.txt ./

RUN pip wheel --wheel-dir=/root/wheels -r requirements.txt

FROM python:3.13.2-alpine3.21 AS production-image

WORKDIR '/app'

COPY --from=build-image /root/wheels /root/wheels
COPY --from=build-image /app/requirements.txt ./

RUN pip install --no-index --find-links=/root/wheels -r requirements.txt

COPY ./ ./

RUN addgroup -S uwsgi && adduser -S uwsgi -G uwsgi

USER uwsgi

CMD ["uwsgi", "--ini", "app.ini"]