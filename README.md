# flask-web-app

头歌《开源代码管理与持续集成》第 5 章 实验 3 —— 关卡 1
「使用 GitHub Actions 将一个基于 Flask 框架的 Python Web 项目自动化部署」

## 目录结构

```
flask-web-app/
├── src/
│   ├── __init__.py
│   └── app.py                  # Flask 核心应用代码
├── tests/
│   └── test_app.py             # 单元测试（unittest）
├── requirements.txt            # 项目依赖清单
├── .github/
│   └── workflows/
│       └── cicd.yml            # GitHub Actions 工作流配置
└── README.md
```

## 本地运行

```bash
pip install -r requirements.txt
python src/app.py          # 访问 http://127.0.0.1:5000
pytest tests/ -v           # 跑单元测试
```

## 自动部署链路

1. 代码推送到 `main` 分支 → 触发 `.github/workflows/cicd.yml`
2. Ubuntu 虚拟环境：拉取代码 → 安装依赖 → `pytest` 自动化测试
3. 通过 SSH 登录头歌服务器 → `git pull` → 安装依赖 → `supervisorctl restart flask-web-app`
4. 通过「服务预览」的外网链接验证：首页返回 `Hello, World!`

## 需要的 GitHub Secrets

| Secret 名称 | 说明 |
| --- | --- |
| `TOUGE_SERVER_IP` | 头歌服务器公网 IP |
| `TOUGE_SSH_PORT` | 头歌服务器 SSH 端口 |
| `TOUGE_SSH_USER` | SSH 用户名（root / coder） |
| `TOUGE_SSH_PRIVATE_KEY` | 本地生成的 RSA 私钥全文（含 BEGIN/END 行） |
