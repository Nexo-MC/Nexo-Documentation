# DialogType

The core of a Dialog is the type of Dialog you want to use.\
The options are [CONFIRM](https://minecraft.wiki/w/Dialog#confirmation), [LIST](https://minecraft.wiki/w/Dialog#dialog_list), [MULTI](https://minecraft.wiki/w/Dialog#multi_action), [NOTICE](https://minecraft.wiki/w/Dialog#notice) & [LINK](https://minecraft.wiki/w/Dialog#server_links)\
The default type is NOTICE

#### DialogAction

Most types have one or more **DialogActions,** which looks as shown below

```yaml
action:
  label: "<red>Action Label"
  tooltip: "<red>Action Tooltip"
  width: 150
```

#### Notice Type

```yaml
type: NOTICE
action:
  ...
```

#### Confirmation Type

Contains two properties, **yes & no**, both which are **DialogActions**

```yaml
type: CONFIRM
yesButton:
  ...
noButton:
  ...
```

#### Dialog List Type

Contains a **DialogAction** property, `exitAction`.\
It also contains `buttonWidth`, `columns` & `dialogs` properties

**buttonWidth -** The width of this button, between 1 -> 1024, defaults to 150\
**columns** - The number of columns, must be 0 or above, defaults to 2\
**dialogs** - A list of Dialog-IDs to display

```yaml
type: LIST
buttonWidth: 150
columns: 2
dialogs:
  - "my_dialog"
exitAction:
  ...
```

#### Multi Action Type

**exitAction -** A **DialogAction**\
**actions -** A list of **DialogActions**\
**columns -** The number of columns, must be 0 or above, defaults to 2

```yaml
type: MULTI
columns: 2
exitAction:
  ...
actions: [ ... ]
```

#### Server Links Type

**buttonWidth -** The width of this button, between 1 -> 1024, defaults to 150\
**columns** - The number of columns, must be 0 or above, defaults to 2\
**exitAction -** A **DialogAction**

```yaml
type: LINK
exitAction:
  ...
columns: 2
buttonWidth: 150
```
