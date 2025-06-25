# Microservices Architecture with Docker and Nginx

A complete microservices architecture featuring Go and Python backend services orchestrated with Docker Compose and load-balanced through an nginx reverse proxy. Deploy the entire stack with just one command. Here are the values of this project

✅ Single command deployment
✅ All services accessible via one port
✅ Automatic health checks
✅ Detailed request logging
✅ Clean architecture separation

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
- **Port**: 8081 (internal)
- **Technology**: Go 

### Python Service  
- **Port**: 8000 (internal)
- **Technology**: Python with Flask/FastAPI

### Nginx Reverse Proxy
- **Port**: 3000 (external)
- **Function**: Load balancing and request routing
- **Configuration**: Routes requests based on URL paths

## 🔧 Configuration

### Environment Variables



# Nginx
NGINX_PORT=80
```

### Nginx Routing

The nginx configuration routes requests as follows:

- `http://localhost:3000/service1/ping* and *http://localhost:3000/service1/hello*` → Go Service (port 8081)
- `http://localhost:3000/service2/ping* and *http://localhost:3000/service2/hello*` → Python Service (port 8000)

## 🧪 Testing the Services

### Health Check Endpoints

```bash
# Test Go service
curl http://localhost:3000/service1/ping
curl http://localhost:3000/service1/hello

# Test Python service  
http://localhost:3000/service2/ping
http://localhost:3000/service2/hello

# Test nginx
curl http://localhost:3000/
http://localhost:3000/health (nginx health)
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



## 🔍 Monitoring and Debugging

### View Container Status
```bash
docker-compose ps
```

### Access Container Logs
```bash
# All services
docker-compose logs
docker-compose logs nginx



```

## 🚦 API Endpoints




## 🛠️ Development

### Local Development Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd microservices-docker-nginx
   ```

2. **Start development environment**
   ```bash
   docker-compose up --build
   ```




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
