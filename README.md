## Structure
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Client    │────│    Nginx    │────│  Service 1  │
│             │    │   (Port 80) │    │   (Go:8001) │
└─────────────┘    │             │    └─────────────┘
                   │             │    ┌─────────────┐
                   │             │────│  Service 2  │
                   └─────────────┘    │(Flask:8002) │
                                      └─────────────┘

- `service_1`: Golang backend
- `service_2`: Python backend
- `nginx`: Reverse proxy for routing

## Usage

```bash
docker-compose up -d
```

- Access Go service: http://localhost:8080/service1/ping http://localhost:8080/service1/hello
- Access Python service: http://localhost:8080/service2/  http://localhost:8080/service2/hello

## Health Checks
http://localhost:8080/nginx-health


Available Endpoints
Service 1 (Go):

GET /service1/ping → {"status": "ok", "service": "1"}
GET /service1/hello → {"message": "Hello from Service 1"}

Service 2 (Python Flask):

GET /service2/ping → {"status": "ok", "service": "2"}
GET /service2/hello → {"message": "Hello from Service 2"}

Nginx:

GET /nginx-health → healthy

Request Flow Example
1. Client: GET http://localhost:8080/service2/ping
2. Nginx: Receives request on port 8080
3. Nginx: Matches /service2/* pattern
4. Nginx: Forwards to http://service_2:8002/ping
5. Service 2: Processes request and returns JSON
6. Nginx: Returns response to client