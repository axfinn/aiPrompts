# Docker Compose 运行项目调试场景 Prompts

## 项目调试准备

### 环境诊断
```
请帮我诊断 [项目名称] 的 Docker Compose 运行环境：

需要检查：
1. Docker 和 Docker Compose 版本兼容性
2. 系统资源（CPU、内存、磁盘空间）
3. 端口占用情况
4. 网络连接状态
5. 必要的环境变量配置
```

### 配置文件验证
```
请验证我的 docker-compose.yml 文件配置：

检查项：
1. YAML 语法正确性
2. 服务依赖关系
3. 环境变量引用
4. 卷挂载路径
5. 网络配置
6. 端口映射冲突
```

## 常见运行问题调试

### 服务启动失败
```
我的 [服务名] 服务无法启动，错误信息为 [错误信息]：

请帮我排查：
1. 镜像拉取或构建问题
2. 容器启动命令错误
3. 依赖服务未就绪
4. 权限问题
5. 资源限制
6. 健康检查失败

调试步骤：
- docker-compose logs [服务名] --tail=100
- docker-compose ps -a
- docker inspect [容器ID]
- docker-compose config
```

### 服务间连接问题
```
[服务A] 无法连接到 [服务B]，报错 [错误信息]：

排查方向：
1. 网络配置
   - 检查是否在同一网络
   - DNS 解析是否正常
   - 使用服务名而非 localhost

2. 端口配置
   - 内部端口 vs 映射端口
   - 防火墙规则

3. 服务启动顺序
   - depends_on 配置
   - 健康检查配置
   - 启动延迟处理

调试命令：
- docker-compose exec [服务A] ping [服务B]
- docker-compose exec [服务A] nslookup [服务B]
- docker network inspect [网络名]
```

### 数据持久化问题
```
我的数据库/存储服务数据丢失了：

检查项：
1. 卷挂载配置
   - 命名卷 vs 绑定挂载
   - 路径权限问题
   - 相对路径 vs 绝对路径

2. 数据备份恢复
   - 数据导出命令
   - 数据导入流程
   - 备份策略

3. 容器生命周期
   - docker-compose down 的影响
   - 卷的保留策略

调试命令：
- docker volume ls
- docker volume inspect [卷名]
- docker-compose exec [服务名] ls -la [数据目录]
```

### 性能和资源问题
```
我的应用运行缓慢或经常崩溃：

性能分析：
1. 资源使用监控
   - CPU 使用率
   - 内存占用
   - 磁盘 I/O
   - 网络带宽

2. 资源限制配置
   - deploy.resources.limits
   - deploy.resources.reservations

3. 日志分析
   - 应用日志
   - 系统日志
   - 慢查询日志

监控命令：
- docker stats
- docker-compose top
- docker system df
- docker-compose logs --tail=1000 | grep -i error
```

## 开发调试技巧

### 热重载配置
```
如何配置 [技术栈] 项目的热重载：

配置要点：
1. 代码目录挂载
2. 开发模式环境变量
3. 文件监听配置
4. 构建缓存优化

示例配置：
- Node.js: nodemon, webpack-dev-server
- Python: Flask debug mode, Django runserver
- Java: Spring Boot DevTools
- PHP: Xdebug
```

### 远程调试设置
```
配置 [IDE/编辑器] 连接到容器内的调试器：

步骤：
1. 暴露调试端口
2. 安装调试依赖
3. 配置调试器
4. IDE 远程调试配置

常见调试端口：
- Node.js: 9229
- Python: 5678
- Java: 5005
- PHP: 9000/9003
```

### 日志管理
```
设置统一的日志收集和查看：

方案：
1. 日志驱动配置
   - json-file
   - syslog
   - fluentd

2. 日志聚合
   - ELK Stack
   - Loki + Grafana
   - 简单文件输出

3. 日志查询
   - docker-compose logs -f
   - docker-compose logs --since="2023-01-01"
   - docker-compose logs [服务名] | grep -i error

日志轮转配置：
logging:
  driver: "json-file"
  options:
    max-size: "10m"
    max-file: "3"
```

## 部署前调试

### 构建优化
```
优化 Docker 镜像构建过程：

优化点：
1. 多阶段构建
2. 层缓存利用
3. 依赖预安装
4. 构建参数使用
5. .dockerignore 配置

构建调试：
- docker-compose build --no-cache [服务名]
- docker-compose build --progress=plain
- docker history [镜像名]
```

### 环境一致性检查
```
确保开发、测试、生产环境一致性：

检查清单：
1. 环境变量差异
   - 必需变量
   - 默认值设置
   - 敏感信息管理

2. 配置文件管理
   - docker-compose.override.yml
   - .env 文件
   - 环境特定配置

3. 依赖版本锁定
   - 基础镜像标签
   - 包管理器锁文件
   - 系统依赖版本
```

### 安全检查
```
Docker Compose 配置安全审查：

审查项：
1. 敏感信息暴露
   - 环境变量中的密码
   - 构建参数中的密钥
   - 日志中的敏感数据

2. 网络安全
   - 不必要的端口暴露
   - 网络隔离配置
   - HTTPS 配置

3. 权限配置
   - 用户权限设置
   - 文件权限
   - 特权模式使用

扫描工具：
- docker scan [镜像名]
- trivy image [镜像名]
```

## 故障恢复

### 快速恢复流程
```
服务异常时的快速恢复步骤：

1. 保存现场
   - docker-compose logs > debug.log
   - docker-compose ps -a > services.txt
   - docker inspect [容器] > container.json

2. 尝试恢复
   - docker-compose restart [服务名]
   - docker-compose up -d --force-recreate [服务名]
   - docker-compose down && docker-compose up -d

3. 数据恢复
   - 检查数据卷完整性
   - 从备份恢复
   - 回滚到上一版本

4. 根因分析
   - 查看错误日志
   - 检查系统资源
   - 分析配置变更
```

### 调试工具集成
```
集成有用的调试工具：

工具容器：
1. 网络调试
   - nicolaka/netshoot
   - 包含: curl, nslookup, ping, tcpdump

2. 数据库客户端
   - adminer
   - phpmyadmin
   - pgadmin

3. 监控工具
   - portainer/portainer-ce
   - 可视化管理界面

使用示例：
docker run --rm -it --network [项目网络] nicolaka/netshoot
```

## 最佳实践建议

### 开发环境配置
```
推荐的开发环境 Docker Compose 配置：

1. 使用 .env.example 模板
2. 配置健康检查
3. 设置重启策略
4. 使用命名卷而非匿名卷
5. 配置日志限制
6. 使用 override 文件分离环境配置
7. 添加有用的 labels
8. 配置合理的停止信号和超时
```

### 调试检查清单
```
系统化的调试流程：

□ 确认 Docker/Docker Compose 版本
□ 验证 docker-compose.yml 语法
□ 检查所有环境变量已设置
□ 确认端口未被占用
□ 验证镜像可以正常拉取/构建
□ 检查服务启动顺序和依赖
□ 查看服务日志寻找错误
□ 验证网络连通性
□ 检查文件权限和卷挂载
□ 监控资源使用情况
□ 测试服务间通信
□ 验证数据持久化
```