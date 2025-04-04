# STEPS TO RUN

1. Make sure you have `docker` in your system.

2. Get the [`docker-compose.yml`](./docker-compose.yml) file.

3. Create a `.env` file in the same folder.

4. Set the env secrets.

```.env
RABBITMQ_URL = amqp://<user>:<password>@host.docker.internal:5672/
RABBITMQ_USER = <user>
RABBITMQ_PASSWORD = <password>
RABBITMQ_QUEUE_NAME = <task_queue_name>

MINIO_ENDPOINT = host.docker.internal:9000
MINIO_ACCESS_KEY = <minio-access-key>
MINIO_SECRET_KEY = <minio-secret-key>

COCKROACHDB_URL = postgresql://root@host.docker.internal:26257/defaultdb?sslmode=disable
MAILER_EMAIL = <mailer-email>
MAILER_PASSWORD = <mailer-password>
FRONTEND_URL = http://host.docker.internal:3000
AUTH_HTTP_PORT = 5000
AUTH_GRPC_PORT = 5001

RUNNER_CONTROLLER_HTTP_PORT = 5002
AUTH_GRPC_ADDRESS = host.docker.internal:5001

NEXT_PUBLIC_BACKEND_BASE_URL=http://localhost:5002
NEXT_PUBLIC_AUTH_BASE_URL=http://localhost:5000
NEXT_PUBLIC_MINIO_BASE_URL=http://localhost:9000
# Set to true and paste token if you want to use AI features.
NEXT_PUBLIC_AI=false
GOOGLE_GENERATIVE_AI_API_KEY=<gemini-api-key>
```

5. Run docker compose to start all containers

```docker
docker compose up
```

6. To stop all containers, Run

```docker
docker compose down
```
