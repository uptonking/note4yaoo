---
title: showmebug-yaoo-work-plan
tags: [showmebug, work]
created: 2024-05-06T02:54:24.884Z
modified: 2024-05-06T02:54:40.374Z
---

# showmebug-yaoo-work-plan

# guide

# plan
- 工作OKR
  - 业务类: ai编程/pr/测试
  - 基建类: 基座工程、代码编辑器
  - 团队类: 测试、运营

- bug
  - 在6月中，初步完成生成需求、task、pr的逻辑和流程
# more

# codebase
- `d42paas_frontend` 项目启动记录
  - cp .env.local.example .env, 然后修改其中的 PAAS_SERVER_RABBITMQ_QUEUE=你的名字， 可不修改queue的名字
  - cd packages/demo; pnpm dev
  - cd packages/server; pnpm dev
  - 修改 packages/server/apps/entry/test/filetree_mock_test 末尾文件名为 filetree_mock
  - 在 http://localhost:3010/ api demo的用户名和手机号可随便写
- `1024code` 注册时要先点击发送验证码，然后在验证码输入框填入6个0就可以注册成功
  - 邀请码测试: hs8MQf, Ukycbf
  - 测试用户是 155572695015和八个一
  - node版本不支持v22，暂时使用v20
  - 编译构建时可通过修改repo文件夹名来避免使用turborepo的cache
