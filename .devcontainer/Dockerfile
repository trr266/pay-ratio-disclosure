FROM python:3.12-slim

COPY requirements.txt .

RUN QUARTO_VERSION=1.4.552 \
    && apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -qq install -y build-essential git clang wget \
    && wget -O quarto.deb https://github.com/quarto-dev/quarto-cli/releases/download/v${QUARTO_VERSION}/quarto-${QUARTO_VERSION}-linux-amd64.deb \
    && dpkg -i quarto.deb \
    && rm quarto.deb \
    && apt-get -qq install -y lmodern \
    && apt-get -qq install -y rsync \
    && quarto install tinytex --quiet

RUN apt-get update && \
    apt-get install -y git && \
    pip install --upgrade pip && \
    pip install -r requirements.txt

COPY docs/ .

CMD ["quarto", "render", "docs", "--no-execute-daemon"]
