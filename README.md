# Go API Gateway 🚀

A lightweight, customizable **API Gateway built with Go** that acts as a single entry point for your microservices. This project demonstrates how to implement routing, reverse proxying, authentication, and extensibility using Go's standard library.

---

## ✨ Features

- 🔀 Dynamic routing to backend services
- 🔁 Reverse proxy using `net/http/httputil`
- 🔐 JWT-based authentication middleware
- 📈 Easy extensibility for rate limiting, logging, and tracing
- 🧩 Clean, modular project structure
- ⚡ Fast and lightweight (pure Go)

---

## 🏗️ Architecture Overview

```
Client
  |
  v
[ Go API Gateway ]
  |        |        |
  v        v        v
UserSvc  OrderSvc  PaymentSvc
```

The gateway inspects the incoming request path, identifies the target service, and proxies the request to the appropriate backend.

---

## 📁 Project Structure

```
api-gateway/
├── main.go
├── config/
│   └── services.go        # Service registry
├── router/
│   └── router.go          # Request routing logic
├── proxy/
│   └── reverse_proxy.go   # Reverse proxy implementation
├── middleware/
│   ├── auth.go            # JWT authentication
│   └── ratelimit.go       # (Optional) rate limiting
└── README.md
```

---

## ⚙️ Configuration

### Service Registry

Define backend services in `config/services.go`:

```go
var Services = map[string]string{
    "user":    "http://localhost:8081",
    "order":   "http://localhost:8082",
    "payment": "http://localhost:8083",
}
```

The first path segment of the request determines the target service.

---

## ▶️ Running the Gateway

### Prerequisites

- Go 1.20+
- Backend services running on configured ports

### Start the Gateway

```bash
go mod tidy
go run main.go
```

The API Gateway will start on:

```
http://localhost:8080
```

---

## 🔌 Example Request Flow

### Incoming Request

```http
GET /user/api/v1/profile
Authorization: Bearer <JWT_TOKEN>
```

### Proxied To

```http
http://localhost:8081/api/v1/profile
```

---

## 🔐 Authentication

The gateway includes a JWT authentication middleware:

- Expects `Authorization: Bearer <token>` header
- Rejects requests without a valid token
- Can be extended to support OAuth2, API keys, or mTLS

---

## 🚦 Rate Limiting (Optional)

Rate limiting can be implemented using:

- `golang.org/x/time/rate`
- Redis-based token bucket (recommended for distributed systems)

---

## 🧪 Testing

You can test using `curl` or Postman:

```bash
curl -H "Authorization: Bearer test-token" \
     http://localhost:8080/user/health
```

---

## 🚀 Future Enhancements

- 📊 Centralized logging (Zap / Logrus)
- 🔍 Distributed tracing (OpenTelemetry)
- 🔄 Circuit breaking & retries
- 📦 Config via YAML / ENV
- ☸️ Kubernetes-ready deployment
- 🔐 mTLS between gateway and services

---

## 🤔 When to Use This Gateway

✅ Good fit if you:
- Want full control and customization
- Prefer lightweight infrastructure
- Are learning or prototyping microservices

❌ Consider tools like **Kong**, **KrakenD**, or **Traefik** if you need:
- Built-in dashboards
- Advanced traffic management
- Enterprise-grade plugins out of the box

---

## 📜 License

MIT License. Feel free to use, modify, and extend.

---

Happy hacking! 😄

