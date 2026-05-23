# 产品需求文档（PRD）- 安心康复

**版本**: v1.0
**更新日期**: 2026-03-07

---

> **⚠️ 文档免责声明**
> 本文档为产品规划参考资料，不提供医疗诊断、治疗或处方服务。文中药物名称、剂量和康复示例均为**原型占位数据**，不可作为临床依据。正式上线前须经具备资质的医疗专业人员审核。遇紧急症状请立即就医。

---

## 产品原则

- **极简主义** - 减少认知负担，每屏一个核心任务
- **老年友好** - 大字体、大按钮、简单操作
- **核心价值** - 提醒 + 督导 + 家属安心

---

# 一、产品概述

## 1.1 产品定位

**产品名称**: 安心康复
**副标题**: 心脏支架术后康复提醒助手
**产品类型**: 微信小程序

## 1.2 产品目标

帮助**冠心病支架术后患者**完成出院后的康复管理，通过数字化手段提升康复依从性，降低家属焦虑。

**核心功能**:
- 用药依从管理
- 康复运动指导
- 症状记录追踪
- 复诊提醒
- 家属远程监护

## 1.3 MVP验证目标

| 验证问题 | 成功标准 |
|---------|---------|
| 老年人是否能独立使用 | 60岁以上用户能在5分钟内完成首次设置 |
| 是否提高用药依从性 | 用药打卡率 >80% |
| 家属是否更安心 | 家属满意度调研 ≥4分（5分制） |

---

# 二、用户画像

## 2.1 主要用户 - 患者

**人口特征**:
- 年龄: 60-90岁
- 病情: 冠脉支架术后康复期
- 技能: 会使用微信，但不熟悉复杂应用

**核心需求**:
- 按时服药提醒（避免遗忘）
- 清晰的每日任务指引
- 复诊时间提醒
- 简单的健康状态记录

**痛点**:
- 记不住多种药物的服用时间
- 不清楚康复阶段该做什么运动
- 担心忘记复诊时间

## 2.2 次要用户 - 家属

**人口特征**:
- 年龄: 30-60岁
- 关系: 子女或配偶
- 场景: 异地或工作繁忙，无法时刻陪伴

**核心需求**:
- 远程查看父母用药情况
- 及时发现异常症状
- 减少每日电话确认的负担

**痛点**:
- 担心父母不按时吃药
- 无法及时了解父母身体状况
- 需要频繁打电话确认

---

# 三、产品架构

## 3.1 角色与关系

```
用户角色:
├── 患者（主要使用者）
└── 家属（监护者，可多人）

关系模型:
一个患者 → 可绑定多个家属
一个家属 → 可监护多个患者
```

## 3.2 功能架构

```
安心康复小程序
├── 患者端
│   ├── 首页（今日任务 + 快捷操作）
│   ├── 用药管理
│   │   ├── 添加/编辑药物
│   │   ├── 用药提醒
│   │   └── 用药记录
│   ├── 康复任务
│   │   ├── 每日任务列表
│   │   └── 任务打卡
│   ├── 健康记录
│   │   ├── 症状记录
│   │   ├── 血压记录
│   │   └── 历史查看
│   ├── 复诊管理
│   │   ├── 复诊时间
│   │   └── 医院信息
│   └── 设置
│       ├── 个人信息
│       └── 家属管理
└── 家属端
    ├── 监护首页
    ├── 患者状态查看
    ├── 异常提醒
    └── 历史记录
```

---

# 四、MVP功能详细设计

## 4.1 首次使用流程

### 流程图
```
进入小程序 → 微信授权 → 选择角色（患者/家属）
    ↓
[患者] 创建档案 → 添加用药 → 设置提醒时间 → 完成
[家属] 扫码/输入邀请码 → 绑定患者 → 完成
```

### 4.1.1 患者档案创建

**必填字段**:
| 字段 | 类型 | 说明 |
|------|------|------|
| 姓名 | 文本输入 | 2-10个字符 |
| 出生年份 | 选择器 | 1930-2010 |
| 手术日期 | 日期选择 | 用于计算康复阶段 |
| 支架数量 | 数字输入 | 1-5个 |

**可选字段**:
| 字段 | 类型 | 说明 |
|------|------|------|
| 诊断 | 多选 | 预设选项（见下） |
| 复诊医院 | 文本输入 | - |
| 主治医生 | 文本输入 | - |

**诊断预设选项**:
- 冠状动脉粥样硬化性心脏病
- 急性心肌梗死
- 不稳定型心绞痛
- 稳定型心绞痛

### 4.1.2 用药信息录入

**添加方式**:
1. **快速选择** - 从常用药物列表选择
2. **手动输入** - 自定义药物信息

**常用药物库**:
| 药物名称 | 默认剂量 | 常见服用时间 |
|---------|---------|------------|
| 阿司匹林 | 100mg | 早餐后 |
| 氯吡格雷 | 75mg | 早餐后 |
| 替格瑞洛 | 90mg | 早晚各一次 |
| 瑞舒伐他汀 | 10mg | 晚餐后 |
| 阿托伐他汀 | 20mg | 晚餐后 |
| 美托洛尔 | 47.5mg | 早餐后 |

**药物信息字段**:
| 字段 | 类型 | 示例 |
|------|------|------|
| 药名 | 文本 | 阿司匹林肠溶片 |
| 剂量 | 文本 | 100mg |
| 服用时间 | 时间选择 | 08:00 |
| 频率 | 单选 | 每日一次/每日两次 |

### 4.1.3 提醒时间设置

**默认提醒时间**:
- 早上: 08:00
- 晚上: 20:00

**提醒方式**:
- 微信订阅消息（需用户授权）
- 小程序内通知

---

## 4.2 用药管理

### 4.2.1 用药提醒

**触发时机**: 到达设定的服药时间

**提醒内容**:
```
【用药提醒】

现在是 08:00，该服药了

今日药物：
• 阿司匹林 100mg
• 氯吡格雷 75mg

[已服用] [稍后提醒]
```

**交互逻辑**:
- 点击"已服用" → 记录服药时间 → 关闭提醒
- 点击"稍后提醒" → 10分钟后再次提醒
- 超过2小时未操作 → 标记为"未服用"，通知家属

### 4.2.2 用药记录查看

**展示维度**:
- 日历视图: 显示每日服药完成情况
- 列表视图: 显示最近7天的详细记录

**记录状态**:
- ✅ 已按时服用
- ⏰ 延迟服用（超过30分钟）
- ❌ 未服用

---

## 4.3 康复任务系统

### 4.3.1 任务生成规则

**基于术后时间自动生成**:

| 康复阶段 | 时间范围 | 运动任务 | 其他任务 |
|---------|---------|---------|---------|
| 早期康复 | 术后0-2周 | 步行5-10分钟 | 避免爬楼、记录血压 |
| 中期康复 | 术后2-4周 | 步行10-20分钟 | 低盐饮食、每日记录 |
| 后期康复 | 术后1-3个月 | 步行30分钟 | 逐步恢复日常活动 |
| 维持期 | 术后3个月+ | 步行30-45分钟 | 定期复查 |

### 4.3.2 任务展示

**首页任务卡片**:
```
今日任务 (2/3)

✅ 早上服药
✅ 步行15分钟
⬜ 记录血压

[去完成]
```

**任务详情页**:
- 任务说明
- 完成方法
- 注意事项
- 打卡按钮

---

## 4.4 健康状态记录

### 4.4.1 症状记录

**记录频率**: 每日一次（建议晚上）

**症状选项**:
| 症状 | 程度选择 |
|------|---------|
| 胸闷 | 无 / 轻微 / 明显 |
| 胸痛 | 无 / 轻微 / 明显 |
| 气短 | 无 / 轻微 / 明显 |
| 头晕 | 无 / 轻微 / 明显 |
| 心悸 | 无 / 轻微 / 明显 |

**快捷记录**:
```
[今天感觉很好]  ← 一键记录"所有症状：无"
```

### 4.4.2 血压记录

**输入字段**:
- 收缩压（mmHg）
- 舒张压（mmHg）
- 测量时间（自动记录）

**异常提示**:
- 收缩压 >140 或 <90 → 提示"血压偏高/偏低，建议咨询医生"
- 舒张压 >90 或 <60 → 同上

### 4.4.3 数据可视化

**图表展示**:
- 血压趋势图（最近7天/30天）
- 症状频率统计
- 用药依从率

---

## 4.5 复诊管理

### 4.5.1 复诊时间自动生成

**基于手术日期计算**:
- 术后1个月
- 术后3个月
- 术后6个月
- 术后12个月

### 4.5.2 复诊提醒

**提醒节点**:
- 提前7天
- 提前3天
- 提前1天
- 当天早上

**提醒内容**:
```
【复诊提醒】

您的复诊时间：2026-04-25

医院：XX医院心内科
医生：XX医生

[查看详情] [已完成复诊]
```

---

## 4.6 家属功能

### 4.6.1 绑定流程

**患者端操作**:
1. 进入"设置" → "家属管理"
2. 点击"邀请家属"
3. 生成邀请二维码或邀请码（有效期7天）

**家属端操作**:
1. 打开小程序 → 选择"我是家属"
2. 扫码或输入邀请码
3. 确认绑定关系（父亲/母亲/配偶等）

### 4.6.2 家属看板

**首页展示**:
```
母亲 - 张XX
术后第45天

今日状态 ✅
✅ 已服药（2/2）
✅ 已步行 20分钟
✅ 已记录血压 120/75

症状：无

[查看详情]
```

**异常提醒**:
```
⚠️ 异常提醒

母亲今日出现胸闷症状
记录时间：14:30

[查看详情] [联系患者]
```

### 4.6.3 历史记录查看

**可查看内容**:
- 用药记录（最近30天）
- 症状记录
- 血压趋势
- 康复任务完成情况

---

# 五、UI/UX设计规范

## 5.1 老年友好设计原则

### 字体规范
- 最小字号: 18px（正文）
- 标题字号: 24-32px
- 关键信息: 加粗显示
- 字体: 系统默认（微软雅黑/苹方）

### 颜色规范
- 主色调: #1AAD19（微信绿，熟悉感）
- 警告色: #FA5151（红色，用于异常提示）
- 成功色: #07C160（绿色，用于完成状态）
- 文字色: #000000（纯黑，高对比度）
- 辅助文字: #888888

### 按钮规范
- 最小点击区域: 88rpx × 88rpx
- 主按钮: 宽度100%，高度88rpx
- 圆角: 8rpx
- 按钮间距: 至少32rpx

### 布局规范
- 页面边距: 32rpx
- 卡片间距: 24rpx
- 内容行高: 1.6倍
- 每屏最多3个操作选项

## 5.2 关键页面原型

### 患者首页
```
┌─────────────────────────┐
│  安心康复                │
│  张XX，术后第45天        │
├─────────────────────────┤
│                         │
│  今日任务 (2/3)         │
│  ✅ 早上服药            │
│  ✅ 步行15分钟          │
│  ⬜ 记录血压            │
│                         │
│  [去完成]               │
│                         │
├─────────────────────────┤
│                         │
│  今日状态               │
│  🙂 今天感觉很好        │
│                         │
│  [记录状态]             │
│                         │
├─────────────────────────┤
│                         │
│  下次复诊               │
│  2026-04-25             │
│  XX医院心内科           │
│                         │
└─────────────────────────┘
```

### 用药提醒弹窗
```
┌─────────────────────────┐
│  ⏰ 用药提醒            │
│                         │
│  现在是 08:00           │
│  该服药了               │
│                         │
│  今日药物：             │
│  • 阿司匹林 100mg       │
│  • 氯吡格雷 75mg        │
│                         │
│  ┌───────────────────┐  │
│  │   已服用          │  │
│  └───────────────────┘  │
│                         │
│  [稍后提醒]             │
│                         │
└─────────────────────────┘
```

---

# 六、数据模型设计

## 6.1 核心数据表

### users（用户表）
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  wechat_openid VARCHAR(100) UNIQUE NOT NULL, -- 微信用户标识，仅服务端保存
  phone VARCHAR(20),
  role VARCHAR(20) NOT NULL, -- 'patient' | 'family'
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### patients（患者档案表）
```sql
CREATE TABLE patients (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  name VARCHAR(50) NOT NULL,
  birth_year INTEGER NOT NULL,
  surgery_date DATE NOT NULL,
  stent_count INTEGER,
  diagnosis JSONB, -- 存储多选诊断
  hospital VARCHAR(100),
  doctor_name VARCHAR(50),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### medications（用药表）
```sql
CREATE TABLE medications (
  id SERIAL PRIMARY KEY,
  patient_id INTEGER REFERENCES patients(id),
  drug_name VARCHAR(100) NOT NULL,
  dose VARCHAR(50),
  schedule_time TIME NOT NULL,
  frequency VARCHAR(20), -- 'once' | 'twice'
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### medication_records（用药记录表）
```sql
CREATE TABLE medication_records (
  id SERIAL PRIMARY KEY,
  medication_id INTEGER REFERENCES medications(id),
  patient_id INTEGER REFERENCES patients(id),
  scheduled_time TIMESTAMP NOT NULL,
  actual_time TIMESTAMP,
  status VARCHAR(20), -- 'taken' | 'missed' | 'delayed'
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### daily_records（每日健康记录表）
```sql
CREATE TABLE daily_records (
  id SERIAL PRIMARY KEY,
  patient_id INTEGER REFERENCES patients(id),
  record_date DATE NOT NULL,
  symptom_chest_pain INTEGER, -- 0:无 1:轻微 2:明显
  symptom_chest_tight INTEGER,
  symptom_breath INTEGER,
  symptom_dizzy INTEGER,
  symptom_palpitation INTEGER,
  blood_pressure_systolic INTEGER,
  blood_pressure_diastolic INTEGER,
  exercise_minutes INTEGER,
  notes TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  UNIQUE(patient_id, record_date)
);
```

### tasks（康复任务表）
```sql
CREATE TABLE tasks (
  id SERIAL PRIMARY KEY,
  patient_id INTEGER REFERENCES patients(id),
  task_date DATE NOT NULL,
  task_type VARCHAR(50), -- 'medication' | 'exercise' | 'record'
  task_content TEXT,
  status VARCHAR(20), -- 'pending' | 'completed'
  completed_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### followups（复诊表）
```sql
CREATE TABLE followups (
  id SERIAL PRIMARY KEY,
  patient_id INTEGER REFERENCES patients(id),
  followup_date DATE NOT NULL,
  hospital VARCHAR(100),
  doctor_name VARCHAR(50),
  status VARCHAR(20), -- 'pending' | 'completed' | 'cancelled'
  notes TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### family_links（家属关系表）
```sql
CREATE TABLE family_links (
  id SERIAL PRIMARY KEY,
  patient_id INTEGER REFERENCES patients(id),
  family_user_id INTEGER REFERENCES users(id),
  relationship VARCHAR(20), -- 'son' | 'daughter' | 'spouse'
  invite_code VARCHAR(20) UNIQUE,
  invite_expires_at TIMESTAMP,
  status VARCHAR(20), -- 'pending' | 'active'
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  UNIQUE(patient_id, family_user_id)
);
```

---

# 七、技术架构

## 7.1 技术栈选型

### 前端（微信小程序）
- **开发框架**: 微信小程序原生开发
- **UI组件库**: Vant Weapp（轻量级组件库）
- **状态管理**: 小程序原生 globalData + 事件总线
- **图表可视化**: uCharts（专为小程序优化）
- **开发工具**: 微信开发者工具

### 后端
- **语言**: Node.js 18+ LTS
- **框架**: Express.js / Koa.js（轻量级，适合快速开发）
- **ORM**: Sequelize（成熟稳定，支持PostgreSQL）
- **认证**: 微信小程序登录 + Session管理
- **定时任务**: node-cron（用于提醒推送）

### 数据库与存储
- **关系型数据库**: PostgreSQL 14+（腾讯云数据库 TencentDB for PostgreSQL）
- **缓存**: Redis 7+（腾讯云数据库 Redis）
- **对象存储**: 腾讯云COS（存储用户头像、报告等文件）

### 云服务（腾讯云）
- **计算**: 云服务器 CVM 或 轻量应用服务器
- **数据库**: TencentDB for PostgreSQL + Redis
- **存储**: 对象存储 COS
- **CDN**: 腾讯云CDN（加速静态资源）
- **消息推送**: 微信订阅消息（官方推送能力）
- **域名备案**: 需完成ICP备案（小程序要求）

### 部署与运维
- **容器化**: Docker + Docker Compose
- **反向代理**: Nginx
- **SSL证书**: 腾讯云SSL证书（免费版）
- **监控**: 腾讯云监控 + 日志服务CLS
- **CI/CD**: Gitee + 腾讯云CODING（国内代码托管）

## 7.2 系统架构图

```
┌──────────────────────────────────────────────┐
│           微信生态（国内）                    │
│  ┌─────────────┐      ┌─────────────┐       │
│  │ 微信小程序   │      │ 微信订阅消息 │       │
│  │  (患者端)   │      │   推送服务   │       │
│  └──────┬──────┘      └──────┬──────┘       │
│         │                    │               │
└─────────┼────────────────────┼───────────────┘
          │ HTTPS (已备案域名) │
          ↓                    ↓
┌──────────────────────────────────────────────┐
│           腾讯云（国内）                      │
│                                              │
│  ┌─────────────┐                            │
│  │   Nginx     │                            │
│  │ (反向代理)   │                            │
│  └──────┬──────┘                            │
│         │                                   │
│         ↓                                   │
│  ┌─────────────┐     ┌──────────────┐      │
│  │  Node.js    │────→│ TencentDB    │      │
│  │  API Server │     │ PostgreSQL   │      │
│  └──────┬──────┘     └──────────────┘      │
│         │                                   │
│         ↓                                   │
│  ┌─────────────┐     ┌──────────────┐      │
│  │   Redis     │     │  腾讯云COS   │      │
│  │  (缓存层)    │     │ (文件存储)   │      │
│  └─────────────┘     └──────────────┘      │
│         ↑                                   │
│         │                                   │
│  ┌──────┴──────┐                            │
│  │  定时任务    │                            │
│  │ (node-cron) │                            │
│  │  提醒推送    │                            │
│  └─────────────┘                            │
│                                              │
└──────────────────────────────────────────────┘
```

**架构说明**:
1. **微信小程序**: 前端运行在微信环境，通过HTTPS调用后端API
2. **域名备案**: 小程序要求服务器域名必须完成ICP备案
3. **腾讯云服务**: 所有后端服务部署在腾讯云（国内节点）
4. **数据库**: 使用腾讯云托管的PostgreSQL和Redis
5. **推送服务**: 使用微信官方订阅消息（无需第三方推送）

## 7.3 核心API设计

### 微信小程序登录认证
```
POST /api/auth/wechat-login
Body: {
  code: string,           // wx.login() 获取的code
  encryptedData: string,  // 用户信息加密数据（可选）
  iv: string              // 加密算法初始向量（可选）
}
Response: {
  token: string,          // 应用会话token；session_key仅服务端保存，不返回前端
  user: User
}
```

### 患者管理
```
POST /api/patients
Body: { name, birth_year, surgery_date, stent_count, ... }
Response: { patient: Patient }

GET /api/patients/:id
Response: { patient: Patient }

PUT /api/patients/:id
Body: { 更新字段 }
Response: { patient: Patient }
```

### 用药管理
```
POST /api/medications
Body: { patient_id, drug_name, dose, schedule_time, frequency }
Response: { medication: Medication }

GET /api/medications?patient_id=:id
Response: { medications: Medication[] }

PUT /api/medications/:id
Body: { 更新字段 }
Response: { medication: Medication }

DELETE /api/medications/:id
Response: { success: boolean }

POST /api/medication-records
Body: { medication_id, status, actual_time }
Response: { record: MedicationRecord }

GET /api/medication-records?patient_id=:id&date=:date
Response: { records: MedicationRecord[] }
```

### 健康记录
```
POST /api/daily-records
Body: {
  patient_id,
  record_date,
  symptom_chest_pain,
  blood_pressure_systolic,
  blood_pressure_diastolic,
  ...
}
Response: { record: DailyRecord }

GET /api/daily-records?patient_id=:id&date=:date
Response: { record: DailyRecord }

GET /api/daily-records/stats?patient_id=:id&period=7d
Response: {
  blood_pressure_trend: [],
  symptom_frequency: {},
  medication_adherence: number
}
```

### 康复任务
```
GET /api/tasks?patient_id=:id&date=:date
Response: { tasks: Task[] }

PUT /api/tasks/:id/complete
Response: { task: Task }
```

### 复诊管理
```
GET /api/followups?patient_id=:id
Response: { followups: Followup[] }

PUT /api/followups/:id
Body: { status, notes }
Response: { followup: Followup }
```

### 家属功能
```
POST /api/family-links/invite
Body: { patient_id }
Response: {
  invite_code: string,
  qr_code_url: string,
  expires_at: timestamp
}

POST /api/family-links/accept
Body: { invite_code, relationship }
Response: { link: FamilyLink }

GET /api/family-links/patients
Response: { patients: Patient[] }

GET /api/family-links/patient-status/:patient_id
Response: {
  patient: Patient,
  today_status: {
    medication_completed: boolean,
    tasks_completed: number,
    symptoms: [],
    blood_pressure: {}
  }
}
```

### 微信订阅消息推送
```
POST /api/notifications/subscribe
Body: {
  patient_id,
  template_id,  // 微信消息模板ID
  scene: string // 订阅场景
}
Response: { success: boolean }

POST /api/notifications/send
Body: {
  wechat_openid: string, // 微信用户标识，仅服务端使用
  template_id: string,
  data: {},
  page: string  // 跳转页面
}
Response: { msgid: string }
```

---

# 八、开发计划

## 8.1 里程碑

| 阶段 | 时间 | 交付物 | 负责人 |
|------|------|--------|--------|
| 需求确认 | 2天 | 最终PRD、原型图 | 产品经理 |
| UI设计 | 3天 | 设计稿、切图资源 | UI设计师 |
| 环境准备 | 1天 | 腾讯云账号、域名备案、小程序注册 | 技术负责人 |
| 后端开发 | 5天 | API接口、数据库设计 | 后端开发 |
| 前端开发 | 5天 | 小程序页面开发 | 前端开发 |
| 联调测试 | 3天 | 功能测试、修复bug | 全员 |
| 内测 | 2天 | 真实用户测试、收集反馈 | 产品+测试 |
| 小程序审核 | 1-3天 | 提交微信审核 | 产品经理 |

**总计**: 约3-4周（22-24个工作日）

## 8.2 人员配置

- 产品经理: 1人（全程）
- UI设计师: 1人（前3天）
- 后端开发: 1人（全程）
- 前端开发: 1人（全程）
- 测试工程师: 0.5人（后期）

## 8.3 前置准备清单

### 微信小程序准备
- [ ] 注册微信小程序账号（需企业主体）
- [ ] 完成小程序认证（300元/年）
- [ ] 配置小程序基本信息（名称、图标、简介）
- [ ] 申请订阅消息模板
- [ ] 配置服务器域名白名单

### 腾讯云准备
- [ ] 注册腾讯云账号（企业实名认证）
- [ ] 购买云服务器（推荐：2核4G，按量计费）
- [ ] 购买PostgreSQL数据库实例
- [ ] 购买Redis实例
- [ ] 申请域名并完成ICP备案（约15-20天）
- [ ] 申请SSL证书（免费版）
- [ ] 配置安全组规则

### 开发工具准备
- [ ] 微信开发者工具
- [ ] Node.js 18+ 环境
- [ ] PostgreSQL客户端（DBeaver/Navicat）
- [ ] Redis客户端（RedisInsight）
- [ ] Git版本控制（Gitee）
- [ ] API测试工具（Postman/Apifox）

### 第三方服务
- [ ] 短信服务（腾讯云短信，备用通知渠道；上线前需取得用户单独同意并提供退订/关闭方式）
- [ ] 对象存储COS（仅在用户主动上传头像、报告等文件时启用；默认不采集影像资料）

---

# 九、风险与应对

## 9.1 技术风险

| 风险 | 影响 | 概率 | 应对措施 |
|------|------|------|---------|
| 域名备案时间过长 | 延迟上线 | 高 | 提前15-20天启动备案流程；使用测试域名先开发 |
| 微信订阅消息送达率低 | 用户收不到提醒 | 中 | 增加小程序内通知；接入腾讯云短信作为备用 |
| 小程序审核不通过 | 无法发布 | 中 | 严格遵守《微信小程序平台运营规范》；避免医疗诊断功能 |
| 老年用户操作困难 | 使用率低 | 高 | 增加新手引导；提供客服支持；简化操作流程 |
| 数据安全问题 | 隐私泄露 | 低 | 数据加密传输；敏感信息脱敏；权限控制 |
| 服务器性能不足 | 响应慢、卡顿 | 低 | 使用Redis缓存；数据库索引优化；CDN加速 |

## 9.2 业务风险

| 风险 | 影响 | 概率 | 应对措施 |
|------|------|------|---------|
| 用户留存率低 | 产品失败 | 中 | 增加打卡激励；家属督促功能；每日推送 |
| 医疗建议不当 | 法律风险 | 中 | 明确免责声明；仅提供提醒服务；不提供诊断建议 |
| 竞品出现 | 市场份额下降 | 低 | 快速迭代；建立用户粘性；医院合作 |
| 推广困难 | 用户增长慢 | 高 | 与医院合作推广；家属口碑传播；社区宣传 |

## 9.3 合规风险

| 风险项 | 要求 | 应对措施 |
|--------|------|---------|
| 小程序类目 | 需选择"医疗-就医服务"类目 | 提供相关资质（如与医院合作协议） |
| 隐私政策 | 必须提供隐私政策页面 | 编写详细的隐私政策并在小程序内展示 |
| 用户协议 | 需用户同意后才能使用 | 首次使用时弹窗确认 |
| 数据安全 | 符合《个人信息保护法》 | 数据加密、最小化收集、用户可删除数据 |
| 医疗免责 | 不得提供诊断、治疗建议 | 明确声明"本产品仅提供健康管理提醒服务" |

---

# 十、成功指标

## 10.1 MVP验证指标

| 指标 | 目标值 | 测量方法 |
|------|--------|---------|
| 每日活跃率 | >60% | 统计每日打开小程序的用户占比 |
| 用药打卡率 | >80% | 统计按时服药记录占比 |
| 任务完成率 | >70% | 统计每日任务完成占比 |
| 家属绑定率 | >50% | 统计绑定家属的患者占比 |
| 用户满意度 | ≥4分 | 问卷调查（5分制） |

## 10.2 长期运营指标

- 月活跃用户数（MAU）
- 用户留存率（次日/7日/30日）
- 平均使用时长
- 功能使用率分布
- NPS（净推荐值）

---

# 十一、未来规划

## V2.0 功能（3-6个月）

### 智能设备集成
- 对接蓝牙血压计、血糖仪等智能设备
- 自动同步测量数据，减少手动输入
- 支持主流品牌：欧姆龙、鱼跃、乐心等

### AI健康助手
- 仅提供健康记录总结、趋势展示和就医提醒，不提供诊断、治疗、处方或用药调整建议
- 异常数据仅提示用户咨询医生或及时就医
- 上线前需完成算法/AI功能风险评估和人工审核机制设计

### 医生端小程序
- 医生可查看患者康复数据
- 远程调整康复计划
- 在线答疑功能

### 社区功能
- 患者交流论坛
- 康复经验分享
- 专家科普文章

### 康复课程
- 康复运动视频教程
- 饮食营养指导
- 心理健康课程

## V3.0 功能（6-12个月）

### 多病种支持
- 扩展到糖尿病、高血压、脑卒中等慢病管理
- 多病种联合管理（如冠心病+糖尿病）

### 商业保险对接
- 与商业保险公司合作
- 康复数据作为保险理赔依据
- 健康管理服务包

### 远程问诊（仅作为远期设想）
- 如涉及在线咨询、电子处方或药品配送，需另行取得医疗机构、医师执业、互联网诊疗、药品经营等相关资质
- 未取得相应资质前，不在产品中提供问诊、诊断、处方或售药能力

### 大数据分析
- 康复效果分析模型
- 风险预警系统
- 个性化康复方案推荐

### 线下服务
- 与康复中心合作
- 上门护理服务
- 康复设备租赁

---

# 附录

## A. 微信小程序开发规范

### A.1 小程序配置文件 (app.json)
```json
{
  "pages": [
    "pages/index/index",
    "pages/medication/medication",
    "pages/tasks/tasks",
    "pages/record/record",
    "pages/followup/followup",
    "pages/family/family",
    "pages/settings/settings"
  ],
  "window": {
    "navigationBarTitleText": "安心康复",
    "navigationBarBackgroundColor": "#1AAD19",
    "navigationBarTextStyle": "white",
    "backgroundColor": "#F8F8F8"
  },
  "tabBar": {
    "color": "#999999",
    "selectedColor": "#1AAD19",
    "backgroundColor": "#FFFFFF",
    "list": [
      {
        "pagePath": "pages/index/index",
        "text": "首页",
        "iconPath": "images/home.png",
        "selectedIconPath": "images/home-active.png"
      },
      {
        "pagePath": "pages/record/record",
        "text": "记录",
        "iconPath": "images/record.png",
        "selectedIconPath": "images/record-active.png"
      },
      {
        "pagePath": "pages/settings/settings",
        "text": "我的",
        "iconPath": "images/user.png",
        "selectedIconPath": "images/user-active.png"
      }
    ]
  },
  "usingComponents": {
    "van-button": "@vant/weapp/button/index",
    "van-cell": "@vant/weapp/cell/index"
  }
}
```

### A.2 订阅消息模板示例

**用药提醒模板**:
```
模板标题：用药提醒
模板内容：
提醒时间：{{time1.DATA}}
药物名称：{{thing2.DATA}}
服用剂量：{{thing3.DATA}}
温馨提示：{{thing4.DATA}}
```

**复诊提醒模板**:
```
模板标题：复诊提醒
模板内容：
复诊时间：{{date1.DATA}}
医院名称：{{thing2.DATA}}
科室医生：{{thing3.DATA}}
温馨提示：{{thing4.DATA}}
```

### A.3 服务器域名配置

需在小程序后台配置以下域名（需完成备案）:
- request合法域名: `https://api.yourdomain.com`
- uploadFile合法域名: `https://upload.yourdomain.com`
- downloadFile合法域名: `https://download.yourdomain.com`

## B. 参考资料

### 医学指南
- 《冠心病介入治疗术后康复指南》（中华医学会）
- 《冠心病合理用药指南》（国家卫健委）
- 《心脏康复与二级预防中国专家共识》

### 设计规范
- 《微信小程序设计指南》
- 《老年人用户体验设计规范》
- 《无障碍设计指南》

### 技术文档
- 微信小程序官方文档: https://developers.weixin.qq.com/miniprogram/dev/framework/
- 腾讯云开发文档: https://cloud.tencent.com/document/product
- Vant Weapp组件库: https://vant-contrib.gitee.io/vant-weapp/

### 法律法规
- 《中华人民共和国个人信息保护法》
- 《互联网信息服务管理办法》
- 《微信小程序平台运营规范》

## C. 术语表

| 术语 | 英文 | 解释 |
|------|------|------|
| PCI | Percutaneous Coronary Intervention | 经皮冠状动脉介入治疗（支架手术） |
| 依从性 | Adherence | 患者按医嘱执行治疗的程度 |
| 双抗 | DAPT | 双联抗血小板治疗（阿司匹林+氯吡格雷） |
| 他汀 | Statin | 降脂药物 |
| MVP | Minimum Viable Product | 最小可行产品 |
| DAU | Daily Active Users | 日活跃用户数 |
| MAU | Monthly Active Users | 月活跃用户数 |
| ICP备案 | - | 互联网内容提供商备案 |
| SSL | Secure Sockets Layer | 安全套接字层（HTTPS加密） |

## D. 成本预算（MVP阶段）

### 开发成本
| 项目 | 单价 | 数量 | 小计 |
|------|------|------|------|
| 产品经理 | 800元/天 | 20天 | 16,000元 |
| UI设计师 | 600元/天 | 5天 | 3,000元 |
| 后端开发 | 1,000元/天 | 15天 | 15,000元 |
| 前端开发 | 1,000元/天 | 15天 | 15,000元 |
| 测试工程师 | 500元/天 | 5天 | 2,500元 |
| **开发小计** | - | - | **51,500元** |

### 云服务成本（首年）
| 项目 | 规格 | 费用 |
|------|------|------|
| 云服务器 | 2核4G | 3,000元/年 |
| PostgreSQL | 1核2G | 2,400元/年 |
| Redis | 1G内存 | 1,200元/年 |
| 对象存储COS | 50GB | 600元/年 |
| CDN流量 | 100GB | 1,000元/年 |
| 短信服务 | 10,000条 | 500元/年 |
| 域名+SSL证书 | - | 200元/年 |
| **云服务小计** | - | **8,900元/年** |

### 其他成本
| 项目 | 费用 |
|------|------|
| 小程序认证费 | 300元/年 |
| 域名备案 | 0元（自行备案） |
| 软件著作权登记 | 300元（可选） |
| **其他小计** | **600元** |

### 总成本
- **MVP开发**: 51,500元
- **首年运营**: 9,500元
- **总计**: 约 **61,000元**

## E. 更新日志

| 版本 | 日期 | 更新内容 | 作者 |
|------|------|---------|------|
| v1.0 | 2026-03-07 | 初始版本，完整PRD文档 | - |

---

**文档状态**: ✅ 已完成优化
**审核状态**: 待审核

---

## 免责声明

本产品仅提供健康管理提醒服务，不提供任何医疗诊断、治疗建议。所有康复计划应在医生指导下进行。如有身体不适，请及时就医。
---

## 发布合规提示

本产品方案仅用于健康管理提醒，不提供医疗诊断、治疗、处方、用药调整或急救服务。所有用药、运动、复诊和康复安排应由用户根据医生医嘱录入或确认；如出现胸痛、胸闷、气短、晕厥、出血等异常情况，应立即就医或联系急救服务。

产品涉及姓名、出生年份、手术日期、诊断、用药记录、症状、血压、医院和医生等医疗健康信息，属于敏感个人信息。正式开发和上线前必须提供用户协议、隐私政策、个人信息收集清单、权限说明、数据删除/导出/注销入口，并在处理敏感个人信息、向家属共享数据、使用短信或云端存储前取得用户单独同意。

医学指南、药物名称、默认剂量、康复任务和阈值仅为产品原型示例，不可作为临床依据。上线前应由具备资质的医疗专业人员审核，并以最新官方指南、药品说明书和医生医嘱为准。