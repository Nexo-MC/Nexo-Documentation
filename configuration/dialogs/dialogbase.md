# DialogBase

Dialogs have a base which contains the content of the Dialog.\
Below are the propeties you can use

**title -** The title of the Dialog, is always visible on the screen\
**externalTitle** - Name used for buttons that link to this Dialog, defaults to title\
**canCloseWithEscape** - If the Dialog can be dismissed with Escape Key\
**afterAction** - Operation performed on the dialog after click or submit actions.\
\* **NONE -** Keeps the current dialog screen open\
\* **CLOSE (Default) -** Close and return to the previous non-dialog screen (if any)\
\* **WAIT\_FOR\_RESPONSE -** Replaces the current screen with a "Waiting for Response"\
**bodies** - List of DialogBodies to add to the Dialog Screen\
**inputs** - List of DialogInputs to add to the Dialog Screen

### [DialogBody](https://minecraft.wiki/w/Dialog#Body_format)

A DialogBody describes content that is positioned between the title and the inputs of the Dialog Screen.\
These are fairly simple and come in two types, MESSAGE & ITEM

**Message-Type** takes a width-property and a string for the message\
This message supports MiniMessage and Nexo Glyphs- & Shift-tags

**Item-Type** has a few more properties.\
**description -** Takes a MiniMessage String and optionally a width (defaults to 200)\
**showDecorations -** When true, shows the count & durability-bar on the item\
**showTooltip -** When true, shows the tooltip when hovering over the item\
**width -** Horizontal size of the element, must be between 1 & 256, defaults to 16\
**height -** Vertical size of the element, must be between 1 & 256, defaults to 16

To make a DialogBody you can follow the below example, specifying a key/id for the Body-element and its properties;

```yaml
base:
  bodies:
    message_body:
      type: MESSAGE
      message: "<red>Some Message allowing MiniMessage"
      width: 200
    item_body:
      type: ITEM
      description: "Some Description"
     #description:
     #  contents: "<red>Some description"
     #  width: 200
      showDecorations: true
      showTooltip: true
      width: 16
      height: 16
```

### [DialogInput](https://minecraft.wiki/w/Dialog#Input_control_format)

DialogInputs are rendered below the DialogBody-elements and have numerous actions for receiving information from players.

There are four types of Inputs, [TEXT](https://minecraft.wiki/w/Dialog#text), [BOOL](https://minecraft.wiki/w/Dialog#boolean), [NUMBER](https://minecraft.wiki/w/Dialog#number_range) & [SINGLE](https://minecraft.wiki/w/Dialog#single_option).

#### Text-Input

A simple text-input field with a few properties\
**width -** The width of the text input field, between 1 & 1024, defaults to 200\
**labelVisible -** Controls if the label is visible for the input-field\
**maxLength** - The max length of the text input\
**initial** - The initial value in the input-field when the Dialog is opened\
**multiLineOptions -** Optional, specifies that the field should be multiline

```yaml
inputs:
  text_key:
    type: TEXT
    width: 200
    label: "<red>Text Input Label"
    labelVisible: true
    maxLength: 32
    initial: "Initial Input Text"
    multilineOptions:
      maxLines: 1
      height: 32
```

#### Boolean-Input

A checkbox returning a string value depending on its state

**onTrue -** The string value to return when checked, default is "true"\
**onFalse -** The string value to return when unchecked, defaults to "false"\
**initial -** The initial state of the checkbox

```yaml
inputs:
  bool_key:  
    type: BOOL
    label: "<red>Boolean Input Label"
    initial: true
    onTrue: "true"
    onFalse: "false"
```

#### NumberRange-Input

A number slider used for returning a number-value

**width -** The width of the slider, between 1 & 1024, defaults to 200\
**labelFormat -** A translation key used for building the label\
**start -** The lowest value of the slider\
**end -** The highest value of the slider\
**step -** The incremental value for each notch on the slider, if unspecified, slider has no notches\
**initial -** The initial value between start & end for the slider when Dialog is shown

```yaml
inputs:
  number_key:
    type: NUMBER
    width: 200
    label: "<red>Number Input Label"
    labelFormat: "options.generic_value"
    start: 0
    end: 1
    initial: 0.5
    step: 0.1
```

#### SingleOption-Input

**labelVisible -** If the label should be visible on the button or not\
**width -** The width of the button\
**options -** A list of SingleOptions the button can have. Contains a **display** text field & an **initial-field**

```yaml
inputs:
  single_key:
    type: SINGLE
    width: 200
    label: "<red>Single Input Label"
    labelVisible: true
    options:
      option_1:
        display: "First Option"
        initial: true
      option_2:
        display: "Second Option"
        initial: false
```
