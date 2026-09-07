# Copyright 2026 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM python:3.12-slim

RUN pip install --no-cache-dir uv==0.8.13

WORKDIR /code

COPY ./pyproject.toml ./README.md ./uv.lock* ./restaurant_data.json ./

COPY ./restaurant_finder ./restaurant_finder
COPY ./images ./images

COPY ./a2ui_agent_sdk-0.5.0-py3-none-any.whl ./
RUN uv sync
RUN uv pip install a2ui_agent_sdk-0.5.0-py3-none-any.whl

ARG AGENT_VERSION=0.0.0
ENV AGENT_VERSION=${AGENT_VERSION}

EXPOSE 8080

CMD ["uv", "run", "python", "-m", "restaurant_finder", "--host", "0.0.0.0", "--port", "8080"]
