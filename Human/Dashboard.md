---
type: dashboard
category: overview
created: {{date}}
---

# 🚀 Command Center

> [!abstract] Welcome Back, Engineer
> **Date**: `$= dv.date('today').toFormat('yyyy-MM-dd')`
> **Focus**: "Build something remarkable today."

---

## 📅 Calendar & Schedule
> [!todo] Today's Timeline
> ```dataview
> LIST
> FROM "Human/DailyNotes"
> WHERE date = date(today)
> ```
*(Tip: Use the "Calendar" plugin to view your daily notes in a monthly grid.)*

---

## 🛠️ Active Task Pipeline
> [!computer] Current Tasks
> ```dataview
> TABLE priority as "P", status as "Status", due_date as "Deadline"
> FROM "Human/Projects/Tasks"
> WHERE status != "✅ Done"
> SORT priority ASC
> ```

---

## 💡 Inspiration & Wisdom
> [!quote] Random Inspiration
> ```dataview
> LIST WITHOUT ID
> "<blockquote>" + content + "</blockquote> — *" + author + "*"
> FROM "Human/Resources/Quotes"
> SORT file.mtime DESC
> LIMIT 1
> ```

---

## 📊 Project Velocity
> [!chart] Sprint Progress
> ```dataviewjs
> const tasks = dv.pages('"Human/Projects/Tasks"').where(p => p.type === 'task');
> const total = tasks.length;
> const done = tasks.where(p => p.status?.includes("✅")).length;
> const progress = total > 0 ? Math.round((done / total) * 100) : 0;
> 
> dv.paragraph(`**Sprint Completion**: ${progress}% (${done}/${total} tasks)`);
> dv.el("progress", "", {attr: {value: progress, max: 100}});
> ```

---
## 🔗 Quick Links
[[Human/Projects/Boards/SprintBoard|🏗️ Kanban Board]] | [[Human/DailyNotes/{{date}}|📅 Today's Log]] | [[Human/Resources/Quotes|📜 Quote Library]]
