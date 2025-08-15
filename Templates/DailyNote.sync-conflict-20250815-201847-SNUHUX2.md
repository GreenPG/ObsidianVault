---
date: "{{date}}"
tags: 
hubs: 
urls:
---

---
date: {{date}}
tags:
    - daily_notes
hubs:
    - "[[]]"
urls:
    -
---

# {{date:dddd D MMMM YYYY}}



## Tasks

### Due Today
```tasks
due today
sort by urgency
```

### Due this week

```tasks
due this week
sort by urgency
```

### Other undone tasks
```tasks
not done
sort by urgency
```

## Log




## Today's notes

```dataview
List FROM "notes" or "zettelkasten" or "inbox" WHERE file.cday = date(today) SORT file.ctime
```

