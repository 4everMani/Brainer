---
type: dashboard
category: overview
created: {{date}}
---

# 🏛️ Human Folder Command Center

> [!info] System Overview
> This dashboard provides a high-level view of your current active projects, tasks, and people.



## 📅 Upcoming Deadlines
```dataview
LIST
FROM "Human/Tasks"
WHERE due_date >= date(today) AND due_date <= date(today) + dur(7 days)
SORT due_date ASC
```

## 📋 Priority Kanban (Simulated)
> [!todo] 🔲 To Do
> ```dataview
> LIST FROM "Human/Projects/Tasks" 
> WHERE status = "todo"
> ```

> [!working] 🔨 In Progress
> ```dataview
> LIST FROM "Human/Tasks" 
> WHERE status = "in-progress"
> ```

> [!done] ✅ Completed
> ```dataview
> LIST FROM "Human/Tasks" 
> WHERE status = "done"
> LIMIT 5
> ```


## 👥 Key Contacts
```dataview
TABLE role as "Role", contact as "Contact"
FROM "Human/People"
LIMIT 5
```

---
