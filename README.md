# Near Far Hub

A full-stack application with React frontend and Laravel backend, containerized with Docker.

## 🏗️ Architecture

- **Frontend**: React application (port 3000)
- **Backend**: Laravel API (port 8000)
- **Database**: MySQL 8.0 (port 3306)
- **Database Admin**: phpMyAdmin (port 8080)

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/) (version 20.0 or higher)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 2.0 or higher)
- [Git](https://git-scm.com/downloads)

## 🚀 Quick Start

### 1. Clone the Repository

Since this project uses Git submodules, you need to clone with the `--recursive` flag:

```bash
git clone --recursive https://github.com/your-username/near-far-hub.git
cd near-far-hub
```

If you've already cloned without `--recursive`, initialize the submodules:

```bash
git submodule update --init --recursive
```

### 2. Environment Setup

The Docker Compose configuration handles most environment variables, but you may need to set up additional configuration files in the submodules:

#### Backend Configuration
```bash
cd backend
cp .env.example .env  # If this file exists
cd ..
```

#### Frontend Configuration
```bash
cd frontend
cp .env.example .env  # If this file exists
cd ..
```

### 3. Build and Start Services

From the root directory, run:

```bash
docker-compose up --build
```

This will:
- Build the frontend and backend Docker images
- Start all services (frontend, backend, database, phpMyAdmin)
- Install dependencies
- Set up the database

### 4. Access the Application

Once all containers are running, you can access:

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8000
- **phpMyAdmin**: http://localhost:8080
- **MySQL Database**: localhost:3306

## 🔧 Development Workflow

### Starting the Application

```bash
# Start all services
docker-compose up

# Start services in background
docker-compose up -d

# View logs
docker-compose logs -f

# View logs for specific service
docker-compose logs -f frontend
docker-compose logs -f backend
```

### Stopping the Application

```bash
# Stop all services
docker-compose down

# Stop and remove volumes (⚠️ This will delete database data)
docker-compose down -v
```

### Running Commands

#### Laravel Backend Commands

```bash
# Access backend container
docker-compose exec backend bash

# Run Laravel artisan commands
docker-compose exec backend php artisan migrate
docker-compose exec backend php artisan cache:clear
docker-compose exec backend php artisan route:list

# Install Composer packages
docker-compose exec backend composer install
```

#### React Frontend Commands

```bash
# Access frontend container
docker-compose exec frontend bash

# Install npm packages
docker-compose exec frontend npm install

# Run tests
docker-compose exec frontend npm test
```

### Database Operations

#### Connect to MySQL

```bash
# Using Docker
docker-compose exec mysql mysql -u root -p api

# Using phpMyAdmin
# Visit http://localhost:8080
# Username: root
# Password: secret
```

#### Reset Database

```bash
# Stop services
docker-compose down

# Remove database volume
docker volume rm near-far-hub_mysql_data

# Restart services
docker-compose up
```

## 🐛 Troubleshooting

### Common Issues

#### Port Already in Use
If you get port conflicts, check what's running on those ports:

```bash
# Check what's using port 3000
lsof -i :3000

# Check what's using port 8000
lsof -i :8000
```

#### Submodules Not Updated
If submodules are empty or outdated:

```bash
git submodule update --init --recursive --remote
```

#### Permission Issues (Linux/Mac)
If you encounter permission issues:

```bash
# Fix ownership (replace 1000:1000 with your user:group)
sudo chown -R 1000:1000 backend frontend
```

#### Container Build Issues
If containers fail to build:

```bash
# Clean Docker cache
docker system prune -a

# Rebuild without cache
docker-compose build --no-cache
```

### Viewing Logs

```bash
# All services
docker-compose logs

# Specific service
docker-compose logs frontend
docker-compose logs backend
docker-compose logs mysql

# Follow logs in real-time
docker-compose logs -f
```

## 🔄 Updating Submodules

To pull the latest changes from both frontend and backend repositories:

```bash
# Update submodules to latest commits
git submodule update --remote

# Commit the submodule updates
git add .
git commit -m "Update submodules to latest versions"
```

## 📊 Database Information

- **Host**: mysql (from containers) / localhost (from host)
- **Port**: 3306
- **Database**: api
- **Username**: root
- **Password**: secret

## 🛠️ Available Scripts

### Root Directory
- `docker-compose up` - Start all services
- `docker-compose down` - Stop all services
- `docker-compose build` - Build all images
- `docker-compose logs` - View all logs

### Backend (Laravel)
- `php artisan migrate` - Run database migrations
- `php artisan serve` - Start Laravel development server
- `composer install` - Install PHP dependencies

### Frontend (React)
- `npm start` - Start development server
- `npm test` - Run tests
- `npm run build` - Build for production

## 📁 Project Structure

```
near-far-hub/
├── backend/              # Laravel backend (submodule)
├── frontend/             # React frontend (submodule)
├── docker-compose.yml    # Docker services configuration
├── .gitmodules          # Git submodules configuration
└── README.md            # This file
```

## 🤝 Contributing

1. Make sure submodules are up to date
2. Create feature branches in the respective submodule repositories
3. Test changes locally using Docker
4. Submit pull requests to the appropriate repository

## 📞 Support

If you encounter any issues:

1. Check the troubleshooting section above
2. View container logs: `docker-compose logs`
3. Ensure all prerequisites are installed
4. Check that ports 3000, 8000, 3306, and 8080 are available