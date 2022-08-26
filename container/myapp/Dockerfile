
FROM public.ecr.aws/lambda/python:3.9.2022.06.01.09-x86_64 as build-stage

WORKDIR /app

COPY pyproject.toml poetry.lock ./

RUN \
    pip install --upgrade pip && \
    pip install poetry && \
    poetry export -f requirements.txt --output requirements.txt

FROM public.ecr.aws/lambda/python:3.9.2022.06.01.09-x86_64 as production-stage

COPY . ${LAMBDA_TASK_ROOT}
COPY --from=build-stage /app/requirements.txt ${LAMBDA_TASK_ROOT}

RUN \
    pip install --upgrade pip && \
    pip install -r requirements.txt

CMD ["app.myfunc.handler"]
