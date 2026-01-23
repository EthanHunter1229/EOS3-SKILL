---
name: invoice-organizer
description: 专业的发票信息提取与费用报销台账生成工具。自动识别发票图片中的关键信息（购买方名称、开票日期、金额、税额、发票号码、发票类型），智能分类排序，按月统计报销总额，生成包含明细和汇总两个工作表的Excel费用报销台账。支持增值税专用发票、普通发票、电子发票等多种类型。使用触发词「整理发票」或「生成费用台账」启动完整处理流程。 当用户需要批量处理发票图片、提取发票信息、生成报销台账或统计报销金额时激活
license: MIT
compatibility: 需要 Python 3.8+ 环境，支持 OpenCV、Tesseract OCR 或云端 OCR API（如百度 OCR、腾讯云 OCR、阿里云 OCR）。适用于处理 JPEG、PNG、PDF 格式的发票图片。
metadata:
  homepage:
  repository:
  tags:
    - 发票识别
    - OCR
    - 财务自动化
    - Excel生成
    - 数据提取
  language: Python
allowed-tools:
  - Read
  - Write
  - Bash
  - Glob
  - Grep
  - Edit
  - WebFetch
  - Task
---

# 发票整理助手

专业的发票信息提取与费用报销台账生成工具。自动识别发票图片中的关键信息（购买方名称、开票日期、金额、税额、发票号码、发票类型），智能分类排序，按月统计报销总额，生成包含明细和汇总两个工作表的Excel费用报销台账。支持增值税专用发票、普通发票、电子发票等多种类型。使用触发词「整理发票」或「生成费用台账」启动完整处理流程。

## 使用场景

当用户需要批量处理发票图片、提取发票信息、生成报销台账或统计报销金额时激活

## 使用说明

=== 发票整理技能参考文档 ===

## 资源文件

### 参考文档

- `resources/ocr-guide.md`: 资源: ocr-guide.md
- `resources/excel-generation.md`: 资源: excel-generation.md
- `resources/invoice-fields.md`: 资源: invoice-fields.md

### 脚本

- `scripts/invoice_ocr.py`: 脚本: invoice_ocr.py
- `scripts/excel_generator.py`: 脚本: excel_generator.py

### 模板

- `templates/invoice_template.json`: 模板: invoice_template.json
- `templates/report_config.json`: 模板: report_config.json

## 调试指南

[调试指南]

---

## 元数据

| 字段 | 值 |
|------|----|
| 版本 | 1.0.0 |
| 作者 |  |

## 更新日志

- **v1.0.0** (2026-01-22): added - 初始版本发布，支持发票OCR识别、信息提取、分类排序、月度统计和Excel台账生成

