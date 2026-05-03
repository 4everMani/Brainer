---
type: task
status: "🔲 To Do"
priority: 1
progress: 0
estimated_time: 60
actual_time: 0
due_date: 2026-05-04
completed_date: 
tags:
  - task
  - todo
  - development
  - UI/UX
  - optimization
created: 2026-05-03
owner: "Me"
project: "[[null]]"
related_notes: [[[MFE]], [[job details]], [[admin-portal]], [[tabs]]]
---

# 📝 Task: Optimize MFE and Admin Portal Details

> [!abstract] Task Context
> **Status**: `$= dv.current().status`
> **Priority**: `$= dv.current().priority == 1 ? "🔴 High" : dv.current().priority == 2 ? "🟡 Medium" : "🔵 Low"`
> **Progress**: `$= (function() { const t = dv.current().file.tasks; const c = t.filter(x => x.completed).length; const total = t.length; const p = total > 0 ? Math.round((c/total)*100) : 0; return "<progress value='" + p + "' max='100'></progress> " + p + "%" })()`
> **Deadline**: `$= dv.current().due_date`

## ⚙️ Configuration
| Property          | Value                                 |
| :---------------- | :------------------------------------ |
| **Status**        | `$= dv.current().status`              |
| **Priority**      | `$= dv.current().priority`            |
| **Estimated Time**| `$= dv.current().estimated_time` min  |
| **Actual Time**   | `$= dv.current().actual_time` min     |
| **Due Date**      | `$= dv.current().due_date`            |
| **Tags**          | `$= dv.current().tags.join(", ")` |

## 🚀 Implementation Plan
- [ ] Review and optimize MFE structure.
- [ ] Adjust pooling period configuration within job details.
- [ ] Implement tab name management and consistency in the admin portal.

## 🔗 Related Notes
`$= dv.current().related_notes.length > 0 ? dv.current().related_notes.join(", ") : "_No related notes linked_"`

## 🗒️ Notes
- Optimize the Micro Frontend (MFE) structure, specifically addressing the pooling period within job details. Additionally, ensure proper handling of tab names within the admin portal, with implementation planned for tomorrow.

---
%%
# 🤖 Automation
```dataviewjs
const tasks = dv.current().file.tasks;
const completed = tasks.filter(t => t.completed).length;
const total = tasks.length;
const percent = total > 0 ? Math.round((completed / total) * 100) : 0;

const file = app.vault.getAbstractFileByPath(dv.current().file.path);
let newStatus = dv.current().status;

// 1. Sync Progress, Status, and Tags in Frontmatter
if (dv.current().progress !== percent) {
    await app.fileManager.processFrontMatter(file, (fm) => {
        fm["progress"] = percent;
        
        let tags = fm["tags"] || [];
        // Remove existing status tags
        tags = tags.filter(t => !["todo", "in-progress", "done"].includes(t));
        
        if (percent === 100) {
            fm["status"] = "✅ Done";
            fm["completed_date"] = new Date().toISOString().split('T')[0];
            newStatus = "✅ Done";
            if (!tags.includes("done")) tags.push("done");
        } else if (percent > 0) {
            fm["status"] = "🚧 In Progress";
            newStatus = "🚧 In Progress";
            if (!tags.includes("in-progress")) tags.push("in-progress");
        } else {
            fm["status"] = "🔲 To Do";
            newStatus = "🔲 To Do";
            if (!tags.includes("todo")) tags.push("todo");
        }
        fm["tags"] = tags;
    });
}

// 2. Sync Kanban Board Position (Self-Healing)
const kanbanPath = "Human/Boards/Task Kanban.md";
const kanbanFile = app.vault.getAbstractFileByPath(kanbanPath);

if (kanbanFile) {
    let content = await app.vault.read(kanbanFile);
    const linkPath = dv.current().file.path;
    const escapedLinkPath = linkPath.replace(/[.*+?^$${}()|[\]\\]/g, '\\$&');
    // Regex to find the task link in the Kanban file, regardless of the alias
    const linkRegex = new RegExp(`^- \\[ \\] \\[\\[${escapedLinkPath}(\\|.*)?\\]\\].*\\n`, 'm');
    const match = content.match(linkRegex);

    if (match) {
        const fullLinkLine = match[0];
        
        // Define section mapping
        const sectionMap = {
            "🔲 To Do": "## 📝 BACKLOG",
            "🚧 In Progress": "## 🚧 IN PROGRESS",
            "✅ Done": "## ✅ DONE"
        };
        
        const targetHeader = sectionMap[newStatus];

        // Only move if the status has actually changed in terms of Kanban sections
        if (targetHeader && !content.includes(`${targetHeader}\n${fullLinkLine.trim()}`)) {
            // Remove from current position
            content = content.replace(linkRegex, "");
            // Add to new position
            content = content.replace(targetHeader, `${targetHeader}\n${fullLinkLine.trim()}\n`);
            await app.vault.modify(kanbanFile, content);
        }
    } else {
        const sectionMap = {
            "🔲 To Do": "## 📝 BACKLOG",
            "🚧 In Progress": "## 🚧 IN PROGRESS",
            "✅ Done": "## ✅ DONE"
        };
        const targetHeader = sectionMap[newStatus];
        const linkText = `[[${dv.current().file.path}|${dv.current().file.name.split('.')[0]}]]`;
        const newLinkLine = `- [ ] ${linkText}\n`;
        if (content.includes(targetHeader)) {
            content = content.replace(targetHeader, `${targetHeader}\n${newLinkLine}`);
            await app.vault.modify(kanbanFile, content);
        }
    }
}
```
%%
