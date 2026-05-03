---
type: dashboard
category: overview
created: 2026-05-03
---

# 🏙️ Brainer Command Center
`$= (function() { const time = new Date().getHours(); const greeting = time < 12 ? "Good Morning" : time < 18 ? "Good Afternoon" : "Good Evening"; return greeting + ", MJaiswal! Ready to crush some tasks today?" })()`

---

## 🧭 Navigation
> [!multi-column]
> > [!abstract] 🗂️ Workspace
> > [[Human/Boards/Task Kanban|📋 Task Kanban]]
> > [[Human/DailyNotes/2026-05-03|📅 Daily Note]]
> > [[Human/Projects/|🏗️ Project Hub]]
>
> > [!todo] ⚡ Quick Actions
> > [[Human/Tasks/Project/|🚀 New Project Task]]
> > [[Human/Tasks/Personal/|👤 New Personal Task]]
> > [[Human/Tasks/Mislenious/|📦 Inbox]]

---

## 📊 Performance Metrics
> [!multi-column]
> > [!summary] 🎯 Task Health
> > `$= (function() { const t = dv.pages('"Human/Tasks"').filter(p => p.type == "task"); return "🔹 " + t.filter(p => p.status != "✅ Done").length + " Active Tasks" })()`
> > `$= (function() { const t = dv.pages('"Human/Tasks"').filter(p => p.type == "task"); return "🔴 " + t.filter(p => p.due_date && p.due_date < dv.date('today') && p.status != "✅ Done").length + " Overdue Tasks" })()`
> > `$= (function() { const t = dv.pages('"Human/Tasks"').filter(p => p.type == "task"); return "✅ " + t.filter(p => p.status == "✅ Done").length + " Completed" })()`
>
> > [!quote] 📈 Progress
> > `$= (function() { const t = dv.pages('"Human/Tasks"').filter(p => p.type == "task"); const total = t.length; if (total === 0) return "0% Global Progress"; let totalSubTasks = 0; let completedSubTasks = 0; t.forEach(p => { const tasks = p.file.tasks; totalSubTasks += tasks.length; completedSubTasks += tasks.filter(x => x.completed).length; }); const avg = totalSubTasks > 0 ? Math.round((completedSubTasks / totalSubTasks) * 100) : 0; return "<progress value='" + avg + "' max='100'></progress> " + avg + "% Global Progress" })()`

---

## 🚀 High-Priority Focus
```dataviewjs
const tasks = dv.pages('"Human/Tasks"')
    .filter(p => p.type == "task" && p.status != "✅ Done" && p.priority == 1)
    .sort(p => p.due_date, 'asc')
    .limit(5);

if (tasks.length > 0) {
    dv.table(
        ["Task", "Project", "Progress", "Deadline"],
        tasks.map(p => {
            const t = p.file.tasks;
            const completed = t.filter(x => x.completed).length;
            const total = t.length;
            const percent = total > 0 ? Math.round((completed / total) * 100) : 0;
            const progressBar = `<progress value="${percent}" max="100"></progress> ${percent}%`;
            
            return [
                p.file.link,
                p.project || "None",
                progressBar,
                p.due_date || "No date"
            ];
        })
    );
} else {
    dv.paragraph("_No high-priority tasks at the moment._");
}
```

---

## 🗓️ Weekly Horizon
> [!multi-column]
> > [!important] 📅 Deadlines (Next 7 Days)
> > ```dataview
> > LIST
> > FROM "Human/Tasks"
> > WHERE type = "task" AND due_date >= date(today) AND due_date <= date(today) + dur(7 days) AND status != "✅ Done"
> > SORT due_date ASC
> > ```
>
> > [!check] ✅ Recent Wins
> > ```dataview
> > LIST
> > FROM "Human/Tasks"
> > WHERE type = "task" AND status = "✅ Done"
> > SORT completed_date DESC
> > LIMIT 5
> > ```

---

## 📂 Category Explorer
> [!multi-column]
> > [!project] 🏗️ Projects
> > ```dataview
> > LIST FROM "Human/Tasks/Project"
> > WHERE type = "task" AND status != "✅ Done"
> > LIMIT 5
> > ```
>
> > [!personal] 👤 Personal
> > ```dataview
> > LIST FROM "Human/Tasks/Personal"
> > WHERE type = "task" AND status != "✅ Done"
> > LIMIT 5
> > ```
>
> > [!misc] 📦 Miscellaneous
> > ```dataview
> > LIST FROM "Human/Tasks/Mislenious"
> > WHERE type = "task" AND status != "✅ Done"
> > LIMIT 5
> > ```

---
%%
# 🤖 System Update
```dataviewjs
// Optional: Auto-refresh stats or logic
```
%%
