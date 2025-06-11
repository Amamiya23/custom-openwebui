# 介绍

这个仓库是我为尝试用 GitHub Action 构建美化后的 OpenWebUI Docker 镜像而创建的




# GitHub Actions 自动构建说明

本项目使用 GitHub Actions 自动构建 Docker 镜像并推送到 Docker Hub。当你推送符合 `v*.*.*` 格式的标签时（例如 `v1.0.0`），会自动触发构建流程。

## 如何配置 GitHub Secrets

如果你 fork 了本项目并希望自动构建推送到自己的 Docker Hub 账号，需要在 GitHub 仓库中设置以下 Secrets：

1. `DOCKERHUB_USERNAME`: 你的 Docker Hub 用户名
2. `DOCKERHUB_TOKEN`: 你的 Docker Hub 访问令牌（不要使用密码，请在 Docker Hub 创建访问令牌）
3. `DOCKERHUB_REPO`: （可选）你希望推送到的仓库名称，默认为 "study"

### 创建 Docker Hub 访问令牌

1. 登录 Docker Hub
2. 点击右上角头像 → Account Settings → Security
3. 点击 "New Access Token"
4. 为令牌命名（例如 "GitHub Actions"）并选择适当的权限（我选择的是 read/write 权限）
5. 复制生成的令牌并保存到 GitHub Secrets

### 在 GitHub 中设置 Secrets

1. 在你 fork 的仓库中，点击 "Settings"
2. 在左侧菜单中选择 "Secrets and variables" → "Actions"
3. 点击 "New repository secret"
4. 添加上述三个 secrets

完成这些设置后，当你推送新的版本标签时，GitHub Actions 将自动构建镜像并推送到你指定的 Docker Hub 仓库。

## 详细的 GitHub Secrets 设置指南

### 第一步：进入仓库设置

<img width="960" alt="image" src="https://github.com/user-attachments/assets/6d37b135-e454-455a-b0bd-4ad4f8002eaf" />

1. 进入你 fork 后的 GitHub 仓库
2. 点击顶部导航栏中的 "Settings" 选项卡

### 第二步：找到 Secrets 设置页面

<img width="356" alt="image" src="https://github.com/user-attachments/assets/5c97c9ba-7170-4697-9f43-bef7bee71584" />

1. 在左侧菜单中找到 "Secrets and variables"
2. 点击展开并选择 "Actions"

### 第三步：添加所需的 Secrets

<img width="797" alt="image" src="https://github.com/user-attachments/assets/1e4b80bb-977c-47ff-a63a-c727fdd2e824" />

对于每个 Secret，点击 "New repository secret" 按钮，然后填写以下信息：

#### 1. DOCKERHUB_USERNAME

- **名称**：DOCKERHUB_USERNAME
- **值**：你的 Docker Hub 用户名
- **示例**：如果你的 Docker Hub 账号是 "myusername"，则填写 "myusername"

#### 2. DOCKERHUB_TOKEN

- **名称**：DOCKERHUB_TOKEN
- **值**：你在 Docker Hub 创建的访问令牌（不是密码）
- **注意**：这是一个敏感信息，创建后将无法再次查看完整令牌，请妥善保存

#### 3. DOCKERHUB_REPO (可选)

- **名称**：DOCKERHUB_REPO
- **值**：你想推送镜像的仓库名称
- **示例**：如果你想推送到 "myusername/myapp"，则填写 "myapp"
- **默认值**：如果不设置此项，将默认使用 "study" 作为仓库名

### 完成设置

添加完所有 Secrets 后，页面将显示如下：

<img width="798" alt="image" src="https://github.com/user-attachments/assets/ac9f79d3-1c95-418c-9c3f-dfe8e11dd550" />

所有这些 Secrets 都会被安全地存储，并且只会在工作流运行时使用，不会暴露在日志或其他可见的输出中。

## 使用示例

### 创建和推送版本标签

要触发自动构建，你需要创建并推送一个符合 `v*.*.*` 格式的Git标签。以下是完整的命令示例：

```bash
# 确保你的更改已提交
git add .
git commit -m "准备发布 v1.0.0"

# 创建标签
git tag v1.0.0

# 推送标签到GitHub（这将触发构建）
git push origin v1.0.0
```
