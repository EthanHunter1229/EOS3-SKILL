# 贡献指南 | Contributing Guide

感谢你考虑为 **图片素材替换生成器** 做出贡献！

## 📋 目录
- [行为准则](#行为准则)
- [如何贡献](#如何贡献)
- [开发流程](#开发流程)
- [代码规范](#代码规范)
- [提交规范](#提交规范)

---

## 行为准则

参与本项目即表示你同意遵守我们的行为准则：
- 尊重所有贡献者
- 接受建设性批评
- 专注于对社区最有利的事情
- 对其他社区成员表现出同理心

---

## 如何贡献

### 报告 Bug 🐛

如果你发现了 bug，请：
1. 检查 [Issues](https://github.com/your-repo/image-material-replacer-skill/issues) 确认是否已被报告
2. 如果没有，创建新 Issue，包含：
   - 清晰的标题和描述
   - 重现步骤
   - 预期行为 vs 实际行为
   - 截图（如适用）
   - 环境信息（操作系统、Karma 版本等）

### 提出新功能 💡

我们欢迎新想法！请：
1. 先在 [Discussions](https://github.com/your-repo/image-material-replacer-skill/discussions) 中讨论
2. 说明功能的价值和用例
3. 等待社区反馈后再开始开发

### 提交代码 🔧

1. **Fork 项目**
   ```bash
   git clone https://github.com/your-username/image-material-replacer-skill.git
   cd image-material-replacer-skill
   ```

2. **创建分支**
   ```bash
   git checkout -b feature/your-feature-name
   # 或
   git checkout -b fix/your-bug-fix
   ```

3. **进行修改**
   - 遵循代码规范
   - 添加必要的测试
   - 更新文档

4. **提交改动**
   ```bash
   git add .
   git commit -m "feat: add amazing feature"
   ```

5. **推送到 GitHub**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **创建 Pull Request**
   - 填写 PR 模板
   - 链接相关 Issue
   - 等待代码审查

---

## 开发流程

### 环境准备

1. **安装 Karma AI**
   ```bash
   npm install -g karma-cli
   karma auth login
   ```

2. **克隆项目**
   ```bash
   git clone https://github.com/your-username/image-material-replacer-skill.git
   cd image-material-replacer-skill
   ```

3. **安装依赖**（如有）
   ```bash
   npm install
   ```

### 测试

在提交 PR 前，请确保：
- [ ] 在 Karma AI 环境中测试通过
- [ ] 所有 4 个步骤正常工作
- [ ] 图片生成质量符合预期
- [ ] 文档更新完整

### 本地测试命令

```bash
# 验证 XML 配置格式
xmllint --noout skill-config.xml

# 在 Karma 中测试技能
karma skill test skill-config.xml
```

---

## 代码规范

### XML 配置规范

- 使用 2 空格缩进
- 属性值使用双引号
- 标签名使用 kebab-case
- 添加必要的注释

```xml
<!-- ✅ 推荐 -->
<step id="1" name="step-name">
  <description>清晰的描述</description>
  <action>
    <type>action-type</type>
  </action>
</step>

<!-- ❌ 不推荐 -->
<step id=1 name=stepName>
<description>描述</description>
<action><type>action-type</type></action></step>
```

### 文档规范

- 使用 Markdown 格式
- 中英文之间加空格
- 代码块指定语言
- 添加必要的示例

---

## 提交规范

我们使用 [Conventional Commits](https://www.conventionalcommits.org/zh-hans/) 规范：

### 提交类型

- `feat`: 新功能
- `fix`: Bug 修复
- `docs`: 文档更新
- `style`: 代码格式（不影响功能）
- `refactor`: 重构（不修复 bug 也不新增功能）
- `perf`: 性能优化
- `test`: 测试相关
- `chore`: 构建过程或辅助工具的变动

### 提交消息格式

```
<type>(<scope>): <subject>

<body>

<footer>
```

### 示例

```bash
# 新功能
git commit -m "feat(generator): add batch generation mode"

# Bug 修复
git commit -m "fix(analysis): resolve prompt extraction error"

# 文档更新
git commit -m "docs(readme): add installation guide"

# 详细提交
git commit -m "feat(generator): add style templates

- Add 5 preset style templates
- Update UI for template selection
- Add template preview feature

Closes #123"
```

---

## Pull Request 检查清单

提交 PR 前，请确认：

- [ ] 代码遵循项目规范
- [ ] 添加了必要的测试
- [ ] 所有测试通过
- [ ] 更新了相关文档
- [ ] 提交消息符合规范
- [ ] PR 标题清晰描述改动
- [ ] 链接了相关 Issue
- [ ] 添加了必要的截图（UI 改动）

---

## 审查流程

1. **自动检查**
   - 代码格式
   - 配置文件验证
   - 文档链接检查

2. **人工审查**
   - 代码质量
   - 功能完整性
   - 文档准确性

3. **合并要求**
   - 至少 1 个维护者批准
   - 所有检查通过
   - 无冲突

---

## 版本发布

由维护者负责：

1. 更新 `CHANGELOG.md`
2. 更新版本号
3. 创建 Git tag
4. 发布 GitHub Release

---

## 联系方式

- **Issue 追踪**: [GitHub Issues](https://github.com/your-repo/image-material-replacer-skill/issues)
- **讨论区**: [GitHub Discussions](https://github.com/your-repo/image-material-replacer-skill/discussions)
- **邮件**: karma@eos3.ai

---

## 致谢

感谢所有贡献者的付出！ 🎉

你的名字将被添加到贡献者列表中。

---

**再次感谢你的贡献！** ❤️
