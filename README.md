# B端师兄认证管理看板

一个用于管理和展示师兄认证进度的数据看板，支持数据导入、多维分析、周报推送等功能。

## 功能特性

- **师兄名单管理**：导入Excel师兄名单，支持搜索、筛选、导出
- **认证进度看板**：实时展示认证状态、部门分布、进度提醒
- **数据导入**：支持多个Excel数据源智能合并
- **周报推送**：一键生成并推送周报到钉钉群
- **数据持久化**：数据存储在服务器，所有人看到同一份数据

## 数据安全方案

**本看板采用脱敏统计数据方案，确保数据安全：**

- **你（管理员）**：在本地导入Excel原始数据，包含姓名、工号、部门等完整信息
- **其他人（查看者）**：打开GitHub Pages链接，只能看到部门分布、认证进度等统计图表，**看不到任何个人信息**
- **导出的stats.json**：只包含部门人数、认证状态统计等数字，不含姓名、工号等敏感信息

## 部署到GitHub Pages

### 步骤1：创建GitHub仓库

1. 访问 https://github.com/new
2. 仓库名填写：`b-end-mentor-board`
3. 设为**Public**（公开仓库才能免费使用GitHub Pages）
4. **不要**勾选"Add README"、".gitignore"、"license"（我们已经有了）
5. 点击"Create repository"

### 步骤2：推送代码到GitHub

在终端执行以下命令（替换`YOUR_USERNAME`为你的GitHub用户名）：

```bash
git remote add origin https://github.com/YOUR_USERNAME/b-end-mentor-board.git
git branch -M main
git push -u origin main
```

### 步骤3：开启GitHub Pages

1. 在GitHub仓库页面，点击"Settings"（设置）
2. 左侧菜单找到"Pages"
3. "Source"选择"GitHub Actions"
4. 保存后，每次推送到main分支都会自动部署

### 步骤4：导出统计数据并上传

1. 在浏览器中打开`index.html`
2. 导入你的Excel数据文件（师兄名单、白领&CCA、爆品团、认证提报）
3. 点击左侧导航栏的"导出统计数据"按钮，下载`stats.json`
4. 将`stats.json`文件复制到项目根目录
5. 提交并推送：

```bash
git add stats.json
git commit -m "更新统计数据"
git push
```

### 步骤5：分享看板链接

部署完成后（通常需要1-2分钟），访问：
```
https://YOUR_USERNAME.github.io/b-end-mentor-board/
```

把这个链接分享给同事，他们看到的是**脱敏后的统计图表**，不包含任何个人信息！

## 更新数据

当Excel数据有变化时：

1. 打开本地`index.html`
2. 重新导入Excel文件
3. 点击"导出统计数据"下载新的`stats.json`
4. 替换项目中的`stats.json`
5. 提交并推送到GitHub

```bash
git add stats.json
git commit -m "更新统计数据"
git push
```

GitHub Pages会在1-2分钟内自动重新部署。

## 本地开发

直接在浏览器中打开`index.html`即可使用。数据会优先从服务器加载`stats.json`（脱敏统计数据），如果没有则使用浏览器localStorage缓存（完整数据）。

## 文件说明

- `index.html` - 看板主页面
- `stats.json` - 脱敏统计数据文件（只包含部门分布、认证状态统计等数字，不含个人信息）
- `.github/workflows/gh-pages.yml` - GitHub Pages自动部署配置

## 注意事项

- GitHub Pages是免费的静态网站托管服务，链接永久有效
- `stats.json`只包含统计数字，不包含姓名、工号等敏感信息
- 更新数据需要重新导出`stats.json`并推送到GitHub
- 原始Excel数据只保存在你本地，不会上传到GitHub
