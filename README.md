# aiPrompts

一个精心策划的 AI 提示集合，用于辅助软件开发各个方面的任务。

![GitHub](https://img.shields.io/github/license/axfinn/aiPrompts)
![GitHub last commit](https://img.shields.io/github/last-commit/axfinn/aiPrompts)
![GitHub issues](https://img.shields.io/github/issues/axfinn/aiPrompts)

## 版本信息

当前版本: v1.2.0

## 目录结构

```
prompts/
├── code_implementation.md     # 通用代码实现提示
├── frontend_development.md    # 前端开发提示
├── backend_development.md     # 后端开发提示
├── devops_deployment.md       # DevOps 和部署提示
└── git_development.md         # Git 开发提示
```

## 内容介绍

### 代码实现提示 (code_implementation.md)
- 通用编程任务（代码解释、优化、调试、重构）
- 特定任务（算法、数据结构、设计模式实现）
- 项目开发（API 设计、数据库设计、完整项目结构）

### 前端开发提示 (frontend_development.md)
- UI 组件开发
- 响应式布局
- 交互功能实现
- 状态管理
- 性能优化
- 数据可视化
- 工程化实践

### 后端开发提示 (backend_development.md)
- API 开发（RESTful、GraphQL）
- 数据库设计与操作
- 身份验证与授权
- 微服务与分布式系统
- 性能与监控

### DevOps 和部署提示 (devops_deployment.md)
- 容器化（Docker、Docker Compose）
- CI/CD 流水线
- 基础设施即代码
- 监控和日志
- 安全加固

### Git 开发提示 (git_development.md)
- 分支管理（功能分支工作流、Git Flow 工作流）
- 提交信息规范（Conventional Commits 规范）
- 版本管理（语义化版本控制）
- 变更记录（CHANGELOG 编写）
- 版本发布（标签管理）
- 代码审查（合并请求审查）
- 冲突解决（合并冲突处理）

## 使用方法

1. 根据你的开发需求选择相应的提示文件
2. 找到适合你场景的提示模板
3. 根据具体需求调整模板中的内容
4. 将提示用于与 AI 助手的交互中

## 开发规范

本项目严格遵循以下开发流程：

1. 所有新功能开发必须在新建的功能分支上进行
2. 开发完成后必须进行代码审查（CR）
3. 审核通过后才能将功能分支合并到主分支
4. 禁止直接在主分支上进行开发
5. 项目采用版本管理，只有在CR通过并合并到主分支时才会触发版本变更、打标签和同步远程仓库

## 贡献

欢迎提交 Issue 或 Pull Request 来改进这些提示模板。

如果你觉得这些提示模板对你有帮助，欢迎请作者喝杯咖啡：

<div align="center">
  <table>
    <tr>
      <td align="center">
        <h3>微信支付</h3>
        <img src="./img/wxpay.JPG" width="200" alt="微信支付二维码">
        <p>微信支付二维码</p>
      </td>
      <td align="center">
        <h3>支付宝</h3>
        <img src="./img/alipay.JPG" width="200" alt="支付宝二维码">
        <p>支付宝二维码</p>
      </td>
    </tr>
  </table>
</div>

感谢您的支持！