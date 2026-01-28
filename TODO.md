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

### 2. 嵌入式预约组件
**优先级**: 中 | **难度**: 中等

当前：点击按钮 → 跳转到 Cal.com 网站
优化后：点击按钮 → 页面内弹出预约窗口

实现代码：
```html
<!-- 在 </body> 前添加 -->
<script src="https://cal.com/embed.js"></script>

<!-- 按钮改成 -->
<button data-cal-link="v1hairsalon">Book Online</button>
```

参考文档: https://cal.com/docs/embed

---

### 3. JSON-LD 结构化数据
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
