# MySQL + Flask Boilerplate Project

This repo contains a boilerplate setup for spinning up 3 Docker containers: 
1. A MySQL 8 container for obvious reasons
1. A Python Flask container to implement a REST API
1. A Local AppSmith Server

## How to setup and start the containers
**Important** - you need Docker Desktop installed

1. Clone this repository.  
1. Create a file named `db_root_password.txt` in the `secrets/` folder and put inside of it the root password for MySQL. 
1. Create a file named `db_password.txt` in the `secrets/` folder and put inside of it the password you want to use for the a non-root user named webapp. 
1. In a terminal or command prompt, navigate to the folder with the `docker-compose.yml` file.  
1. Build the images with `docker compose build`
1. Start the containers with `docker compose up`.  To run in detached mode, run `docker compose up -d`. 

name: CI/CD Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.9'
        
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2
        
    - name: Build Docker images
      run: docker compose build
      
    - name: Run Tests
      run: |
        # 创建必要的密钥文件
        mkdir -p secrets
        echo "your_root_password" > secrets/db_root_password.txt
        echo "your_webapp_password" > secrets/db_password.txt
        
        # 启动 Docker 容器
        docker compose up -d
        
        # 等待服务启动
        sleep 30
        
        # 运行测试（需要在项目中添加测试脚本）
        # docker compose exec flask python -m pytest
        
    - name: Stop containers
      if: always()
      run: docker compose down

  deploy:
    needs: build-and-test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
    - name: Deploy to production
      run: |
        echo "部署步骤将根据实际部署环境配置"
        # 这里添加实际的部署命令


