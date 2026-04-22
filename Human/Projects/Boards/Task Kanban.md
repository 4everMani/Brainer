---

kanban-plugin: board
board_name: Projects & Tasks Board
display_type: kanban

---

## 📝 Backlog

- [ ] ```dataview
	LIST
	FROM "Human/Projects/Tasks"
	WHERE status = "todo"
	GROUP BY file.link
	SORT file.link ASC
	LIMIT 100


## 🚧 In Progress

- [ ] ```dataview
	LIST
	FROM "Human/Projects/Tasks"
	WHERE status = "in-progress"
	GROUP BY file.link
	SORT file.link ASC
	LIMIT 100


## 👀 Review

- [ ] ```dataview
	LIST
	FROM "Human/Projects/Tasks"
	WHERE status = "review"
	GROUP BY file.link
	SORT file.link ASC
	LIMIT 100


## ✅ Done

- [ ] ```dataview
	LIST
	FROM "Human/Projects/Tasks"
	WHERE status = "done"
	GROUP BY file.link
	SORT file.link ASC
	LIMIT 100




%% kanban:settings
```
{"kanban-plugin":"board","list-collapse":[]}
```
%%