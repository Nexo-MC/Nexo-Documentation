---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# DialogAction

DialogActions are divided in two types, **Static & Dynamic**.\
Static-actions do not depend on the value of an input field.\
Dynamic-actions can be used in conjunction with the value of input fields.

### Static Actions

Types of static-actions are [OPEN\_URL](https://minecraft.wiki/w/Dialog#open_url), [RUN\_COMMAND](https://minecraft.wiki/w/Dialog#run_command), [SUGGEST\_COMMAND](https://minecraft.wiki/w/Dialog#suggest_command), [CHANGE\_PAGE](https://minecraft.wiki/w/Dialog#change_page), [CLIPBOARD](https://minecraft.wiki/w/Dialog#copy_to_clipboard), [SHOW\_DIALOG](https://minecraft.wiki/w/Dialog#show_dialog) and [CUSTOM](https://minecraft.wiki/w/Dialog#custom)

```yaml
action:
  type: RUN_COMMAND
  command: "nexo inventory"
```

### Dynamic Actions

Dynamic actions are actions that can be used with values of input fields in the dialog.\
For example run a command with text from the DialogInput Text field\
The types of dynamic actions are [DYNAMIC\_RUN\_COMMAND](https://minecraft.wiki/w/Dialog#dynamic/run_command) & [DYNAMIC\_CUSTOM](https://minecraft.wiki/w/Dialog#dynamic/custom)
