---
name: code_review_tv
description: TV项目全量代码评审，对照spec规范检查架构、编码、TV适配问题
allowed-tools: [file-read,lint]
---
检查项：MVVM分层混乱、硬编码尺寸、焦点缺失、触屏不兼容、SDK版本违规、弃用API
输出：问题清单+优化代码片段