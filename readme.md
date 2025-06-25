# Microservices Architecture with Docker and Nginx

A complete microservices architecture featuring Go and Python backend services orchestrated with Docker Compose and load-balanced through an nginx reverse proxy. Deploy the entire stack with just one command.

## 🏗️ Architecture Overview

This project demonstrates a production-ready microservices setup with:

- **Go Service**: High-performance backend service
- **Python Service**: Feature-rich backend service  
- **Nginx Reverse Proxy**: Load balancing and routing
- **Docker Compose**: Complete orchestration

## 📁 Project Structure

```
microservices-docker-nginx/
├── docker-compose.yml          # Main orchestration file
├── nginx/
│   ├── Dockerfile
│   └── nginx.conf             # Reverse proxy configuration
├── go-service/
│   ├── Dockerfile
│   ├── go.mod
│   ├── go.sum
│   └── main.go               # Go application
├── python-service/
│   ├── Dockerfile
│   ├── requirements.txt
│   └── app.py               # Python application
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- Docker (20.10+)
- Docker Compose (2.0+)

### One-Command Deployment

```bash
docker-compose up --build
```

That's it! The entire microservices stack will be running and accessible.

## 📋 Services

### Go Service
- **Port**: 8080 (internal)
- **Technology**: Go with Gin framework
- **Endpoints**: `/api/go/*`

### Python Service  
- **Port**: 8000 (internal)
- **Technology**: Python with Flask/FastAPI
- **Endpoints**: `/api/python/*`

### Nginx Reverse Proxy
- **Port**: 80 (external)
- **Function**: Load balancing and request routing
- **Configuration**: Routes requests based on URL paths

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the root directory:

```env
# Go Service
GO_PORT=8080
GO_ENV=production

# Python Service  
PYTHON_PORT=8000
PYTHON_ENV=production

# Nginx
NGINX_PORT=80
```

### Nginx Routing

The nginx configuration routes requests as follows:

- `/api/go/*` → Go Service (port 8080)
- `/api/python/*` → Python Service (port 8000)
- `/` → Static content or default service

## 🧪 Testing the Services

### Health Check Endpoints

```bash
# Test Go service
curl http://localhost/api/go/health

# Test Python service  
curl http://localhost/api/python/health

# Test nginx
curl http://localhost/
```

### Load Testing

```bash
# Install Apache Bench (if not already installed)
# Ubuntu/Debian: apt-get install apache2-utils
# macOS: brew install httpie

# Test load balancing
ab -n 1000 -c 10 http://localhost/api/go/
ab -n 1000 -c 10 http://localhost/api/python/
```

## 🐳 Docker Commands

### Build and Run
```bash
# Build and start all services
docker-compose up --build

# Run in detached mode
docker-compose up -d --build

# View logs
docker-compose logs -f

# Stop all services
docker-compose down
```

### Individual Service Management
```bash
# Rebuild specific service
docker-compose build go-service
docker-compose build python-service
docker-compose build nginx

# Scale services
docker-compose up --scale go-service=3 --scale python-service=2
```

## 🔍 Monitoring and Debugging

### View Container Status
```bash
docker-compose ps
```

### Access Container Logs
```bash
# All services
docker-compose logs

# Specific service
docker-compose logs go-service
docker-compose logs python-service
docker-compose logs nginx
```

### Execute Commands in Containers
```bash
# Access Go service container
docker-compose exec go-service /bin/sh

# Access Python service container
docker-compose exec python-service /bin/bash

# Access Nginx container
docker-compose exec nginx /bin/bash
```

## 🚦 API Endpoints

### Go Service Endpoints
- `GET /api/go/health` - Health check
- `GET /api/go/users` - Get all users
- `POST /api/go/users` - Create user
- `GET /api/go/users/{id}` - Get user by ID

### Python Service Endpoints  
- `GET /api/python/health` - Health check
- `GET /api/python/data` - Get data
- `POST /api/python/process` - Process data
- `GET /api/python/status` - Service status

## 🛠️ Development

### Local Development Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd microservices-docker-nginx
   ```

2. **Start development environment**
   ```bash
   docker-compose -f docker-compose.dev.yml up --build
   ```

3. **Make changes and rebuild**
   ```bash
   docker-compose build <service-name>
   docker-compose up -d <service-name>
   ```

### Adding New Services

1. Create service directory with Dockerfile
2. Add service to `docker-compose.yml`
3. Update nginx configuration for routing
4. Rebuild and deploy

## 🔐 Security Considerations

- Services communicate through internal Docker network
- Only nginx exposes external ports
- Environment variables for sensitive configuration
- Health checks for service monitoring
- Resource limits defined in docker-compose.yml

## 📊 Performance Optimization

- **Nginx**: Configured for optimal load balancing
- **Docker**: Multi-stage builds reduce image size
- **Services**: Horizontal scaling supported
- **Caching**: Redis can be added for session management

## 🚨 Troubleshooting

### Common Issues

**Port Already in Use**
```bash
# Find process using port 80
sudo netstat -tulpn | grep :80
# Kill process or change port in docker-compose.yml
```

**Service Won't Start**
```bash
# Check logs
docker-compose logs <service-name>
# Rebuild from scratch
docker-compose down
docker-compose build --no-cache
docker-compose up
```

**Cannot Connect to Services**
```bash
# Verify all containers are running
docker-compose ps
# Check nginx configuration
docker-compose exec nginx nginx -t
```

## 📈 Scaling and Production

### Production Deployment

1. **Use production docker-compose file**
   ```bash
   docker-compose -f docker-compose.prod.yml up -d
   ```

2. **Set up monitoring** (Prometheus + Grafana)
3. **Configure SSL/TLS** with Let's Encrypt
4. **Set up CI/CD pipeline**
5. **Implement health checks and alerting**

### Horizontal Scaling
```bash
# Scale services based on load
docker-compose up --scale go-service=5 --scale python-service=3
```

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -am 'Add new feature'`
4. Push to branch: `git push origin feature/new-feature`
5. Submit pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙋‍♂️ Support

- **Issues**: [GitHub Issues](https://github.com/your-repo/issues)
- **Documentation**: [Wiki](https://github.com/your-repo/wiki)
- **Discussions**: [GitHub Discussions](https://github.com/your-repo/discussions)

---

**Built with ❤️ using Docker, Go, Python, and Nginx**
