# Distributed Image Processing System

A distributed image-processing pipeline built to practice asynchronous job processing, worker concurrency, object storage, persistent metadata, and performance benchmarking.

## Planned Architecture

- API/coordinator: Java + Spring Boot
- Queue: RabbitMQ
- Workers: C++ + OpenCV
- Storage: S3-compatible object storage with MinIO
- Metadata: PostgreSQL
- Deployment: Docker Compose
- Load testing: k6
