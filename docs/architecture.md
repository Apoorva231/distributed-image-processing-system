# Architecture

## Goal

Build a distributed image-processing system where clients submit image jobs to an API, jobs are processed asynchronously by worker processes, and results are stored for later retrieval.

## Components

### API / Coordinator

The API receives image-processing requests, stores job metadata, uploads original images to object storage, and publishes work messages to the queue.

Technology: Java + Spring Boot

### Queue

The queue decouples the API from the workers. The API can accept jobs quickly while workers process them independently.

Technology: RabbitMQ

### Workers

Workers consume jobs from the queue, download input images, process them, upload outputs, and update job status.

Technology: C++ + OpenCV

### Object Storage

Object storage holds original images and processed outputs.

Technology: MinIO, using the S3 API

### Metadata Store

The metadata store tracks job IDs, job states, input paths, output paths, attempts, timestamps, and errors.

Technology: PostgreSQL

## Reliability Goals

- Jobs should survive API restarts.
- Jobs should survive worker crashes.
- A job may be delivered more than once, so processing must be idempotent.
- Failed jobs should be retried safely.
- Permanently failing jobs should be visible for debugging.
