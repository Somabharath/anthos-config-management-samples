# Copyright 2024 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Build stage
FROM golang:1.24 as builder

WORKDIR /
COPY . .

# Set GOPATH
ENV GOPATH=/go

# Build the webhook server binary for Linux
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o webhook-server main.go

# Final stage
FROM gcr.io/distroless/static:nonroot

WORKDIR /

# Copy the built binary from the builder stage
COPY --from=builder /webhook-server /webhook-server

CMD ["/webhook-server"]