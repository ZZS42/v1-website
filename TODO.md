# V1 Hair Salon - 后续优化任务

> 创建于 2026-01-27 | 预约功能已完成基础版本

---

## 待办优化

### 1. Cal.com 事件名称优化
**优先级**: 高 | **难度**: 简单

当前名称：
- "30 min meeting"
- "15 min meeting"

建议改成：
- "Haircut - 剪发" ($45, 30min)
- "Color - 染发" ($120, 60min)
- "Styling - 造型" ($50, 30min)

**操作位置**: Cal.com 后台 → Event Types → 点击编辑

---

### 2. Embed Fallback 方案
**优先级**: 低 | **难度**: 中等

当前：如果 Cal.com embed.js 加载失败，按钮无响应
优化后：检测加载失败，降级为普通链接跳转

实现思路：
```javascript
// 检测 Cal.com 是否加载成功
if (!window.Cal) {
  // 降级：把 button 替换为 <a> 链接
  document.querySelectorAll('[data-cal-link]').forEach(btn => {
    btn.onclick = () => window.open('https://cal.com/v1hairsalon', '_blank');
  });
}
```

### 3. SMS 短信通知（老板端）
**优先级**: 高 | **难度**: 中等

架构：Cal.com Webhook → Cloudflare Worker → Twilio SMS → 老板手机

成本估算：~$26/月（10 店）

待办：
- [ ] 注册 Twilio 账号
- [ ] 创建 Cloudflare Worker
- [ ] 配置 Cal.com Webhook

---

### 4. JSON-LD 结构化数据
**优先级**: 低 | **难度**: 简单

在现有 JSON-LD 中添加预约入口：
```json
"potentialAction": {
  "@type": "ReserveAction",
  "target": {
    "@type": "EntryPoint",
    "urlTemplate": "https://cal.com/v1hairsalon"
  }
}
```

效果：Google 搜索结果可能显示预约按钮

---

## 已完成

- [x] Hero 区域 Book Online 按钮
- [x] Contact 区域 Book Online 按钮
- [x] Cal.com 集成 (v1hairsalon)
- [x] **嵌入式预约组件** (点击按钮 → 页面内弹出)
- [x] 测试通过 (10/10)
- [x] Lint 通过
- [x] PR #1 创建

---

## 参考项目 (已下载到 references/)

- `cal.com/` - 完整预约系统源码
- `supabase/` - 后端数据库
- `react-hook-form/` - 表单处理
- `novu/` - 通知系统

---

*下次继续时，说"继续优化预约功能"即可*
