# API 文档 | API Documentation

本文档描述"图片素材替换生成器"技能的技术接口和集成方式。

---

## 概述

本技能基于 Karma AI Skill Framework，采用 XML 配置驱动的工作流架构。

---

## 技能配置结构

### 基础元数据

```xml
<skill>
  <metadata>
    <name>技能名称</name>
    <description>技能描述</description>
    <version>版本号</version>
    <author>作者</author>
    <category>分类</category>
    <tags>标签1,标签2</tags>
  </metadata>

  <workflow>
    <!-- 工作流定义 -->
  </workflow>
</skill>
```

### 工作流步骤

```xml
<step id="步骤ID" name="步骤名称">
  <description>步骤描述</description>

  <action>
    <type>动作类型</type>
    <!-- 动作参数 -->
  </action>

  <!-- 可以有多个 action -->
</step>
```

---

## 动作类型 (Action Types)

### 1. request_image_upload

请求用户上传图片

```xml
<action>
  <type>request_image_upload</type>
  <prompt>请上传图片</prompt>
  <variable>image_var</variable>
</action>
```

**参数**:
- `prompt` (string): 提示文本
- `variable` (string): 存储变量名

**返回**: 图片 base64 数据存储在指定变量中

---

### 2. request_text_input

请求用户输入文本

```xml
<action>
  <type>request_text_input</type>
  <prompt>请输入文本</prompt>
  <variable>text_var</variable>
  <required>true</required>
  <multiline>false</multiline>
</action>
```

**参数**:
- `prompt` (string): 提示文本
- `variable` (string): 存储变量名
- `required` (boolean): 是否必填
- `multiline` (boolean): 是否多行

**返回**: 用户输入的文本

---

### 3. call_skill

调用其他技能

```xml
<action>
  <type>call_skill</type>
  <skill_name>其他技能名称</skill_name>
  <input>
    <param1>${variable1}</param1>
    <param2>固定值</param2>
  </input>
  <output_variable>result_var</output_variable>
</action>
```

**参数**:
- `skill_name` (string): 要调用的技能名称
- `input` (object): 输入参数
- `output_variable` (string): 结果存储变量

**返回**: 被调用技能的返回值

---

### 4. call_tool

调用 MCP 工具

```xml
<action>
  <type>call_tool</type>
  <tool>mcp__tool-gateway__gemini_generate_image</tool>
  <parameters>
    <prompt>${final_prompt}</prompt>
    <aspectRatio>16:9</aspectRatio>
    <imageSize>4K</imageSize>
  </parameters>
  <output_variable>generated_image</output_variable>
</action>
```

**参数**:
- `tool` (string): MCP 工具名称
- `parameters` (object): 工具参数
- `output_variable` (string): 结果存储变量

**可用工具**:
- `mcp__tool-gateway__gemini_generate_image`: Gemini 图像生成
- `mcp__tool-gateway__local_generate_image`: 本地图像生成
- `mcp__tool-gateway__sovereign_generate_image`: 主权 AI 图像生成

---

### 5. analyze_image

分析图片内容

```xml
<action>
  <type>analyze_image</type>
  <input>${image_var}</input>
  <extract>主要元素、颜色、风格</extract>
  <output_variable>analysis_result</output_variable>
</action>
```

**参数**:
- `input` (string): 图片变量
- `extract` (string): 要提取的信息
- `output_variable` (string): 结果存储变量

**返回**: 图片分析结果文本

---

### 6. compose_prompt

组合提示词

```xml
<action>
  <type>compose_prompt</type>
  <template>
标题: ${title}
描述: ${description}
风格: ${style}
  </template>
  <output_variable>final_prompt</output_variable>
</action>
```

**参数**:
- `template` (string): 提示词模板（支持变量替换）
- `output_variable` (string): 结果存储变量

**返回**: 组合后的提示词文本

---

### 7. display_result

显示结果

```xml
<action>
  <type>display_result</type>
  <message>
✅ 操作完成！
结果: ${result_var}
  </message>
</action>
```

**参数**:
- `message` (string): 显示消息（支持变量替换和 Markdown）

**返回**: 无返回值，仅展示

---

## 变量系统

### 变量作用域

- 变量在整个 workflow 中全局可用
- 使用 `${variable_name}` 语法引用
- 支持嵌套引用

### 内置变量

- `${workflow.id}`: 当前工作流 ID
- `${workflow.step}`: 当前步骤号
- `${user.id}`: 用户 ID
- `${timestamp}`: 当前时间戳

---

## 集成方式

### 方式1：通过对话触发

```javascript
// 用户在对话中说：
"使用图片素材替换生成器"

// 或者：
"调用 image-material-replacer-skill"
```

### 方式2：通过 API 调用

```javascript
const karma = require('karma-sdk');

// 执行技能
const result = await karma.skills.execute({
  skillName: 'image-material-replacer-skill',
  inputs: {
    // 可选：预先提供输入
    example_image: imageBase64,
    new_title: '春季新品',
    // ...
  }
});

console.log(result.generated_image);
```

### 方式3：嵌入其他技能

```xml
<action>
  <type>call_skill</type>
  <skill_name>image-material-replacer-skill</skill_name>
  <input>
    <example_image>${my_image}</example_image>
  </input>
  <output_variable>new_image</output_variable>
</action>
```

---

## 错误处理

### 错误类型

1. **ValidationError**: 参数验证失败
   ```json
   {
     "error": "ValidationError",
     "message": "参数 'prompt' 不能为空",
     "code": "INVALID_PARAM"
   }
   ```

2. **ToolExecutionError**: 工具执行失败
   ```json
   {
     "error": "ToolExecutionError",
     "message": "图片生成超时",
     "code": "TIMEOUT"
   }
   ```

3. **SkillNotFoundError**: 技能未找到
   ```json
   {
     "error": "SkillNotFoundError",
     "message": "未找到技能: 图片提示词反向分析器",
     "code": "SKILL_NOT_FOUND"
   }
   ```

### 错误处理示例

```xml
<action>
  <type>call_tool</type>
  <tool>mcp__tool-gateway__gemini_generate_image</tool>
  <parameters>...</parameters>
  <output_variable>result</output_variable>
  <on_error>
    <action>
      <type>display_result</type>
      <message>❌ 生成失败，请重试</message>
    </action>
  </on_error>
</action>
```

---

## 性能优化

### 缓存机制

```xml
<action>
  <type>call_skill</type>
  <skill_name>图片提示词反向分析器</skill_name>
  <cache_enabled>true</cache_enabled>
  <cache_ttl>3600</cache_ttl>
</action>
```

### 异步执行

```xml
<action>
  <type>call_tool</type>
  <tool>mcp__tool-gateway__gemini_generate_image</tool>
  <async>true</async>
  <timeout>120000</timeout>
</action>
```

---

## 钩子函数

### before_step

步骤执行前触发

```xml
<step id="4" name="生成新图片">
  <before_step>
    <action>
      <type>display_result</type>
      <message>⏳ 准备生成图片...</message>
    </action>
  </before_step>

  <!-- 正常步骤内容 -->
</step>
```

### after_step

步骤执行后触发

```xml
<step id="4" name="生成新图片">
  <!-- 正常步骤内容 -->

  <after_step>
    <action>
      <type>call_tool</type>
      <tool>karma_save_note</tool>
      <parameters>
        <title>生成记录</title>
        <content>${final_prompt}</content>
      </parameters>
    </action>
  </after_step>
</step>
```

---

## 扩展开发

### 自定义动作类型

创建 `custom-actions.js`:

```javascript
module.exports = {
  // 自定义动作：优化提示词
  optimize_prompt: async (context, params) => {
    const originalPrompt = params.input;

    // 调用优化逻辑
    const optimized = await aiOptimize(originalPrompt);

    return {
      [params.output_variable]: optimized
    };
  }
};
```

在配置中使用:

```xml
<action>
  <type>optimize_prompt</type>
  <input>${original_prompt}</input>
  <output_variable>optimized_prompt</output_variable>
</action>
```

---

## 版本兼容性

| Skill Version | Karma AI Version | 兼容性 |
|---------------|------------------|--------|
| 1.0.0         | >= 2.0.0         | ✅ 完全兼容 |
| 1.0.0         | 1.x              | ⚠️ 部分功能不可用 |

---

## 更多资源

- [Karma AI Skill Framework 文档](https://docs.karma.eos3.ai/skills)
- [MCP 工具参考](https://docs.karma.eos3.ai/mcp-tools)
- [示例代码仓库](https://github.com/eos3-community/karma-skills)

---

**有问题？** 查看 [FAQ](../README.md#faq) 或提交 [Issue](https://github.com/your-repo/image-material-replacer-skill/issues)
