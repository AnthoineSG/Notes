# Theme perso VSCode

## Customisation de vsc

```json
{
  "workbench.colorCustomizations": {
    "editor.background": "#273136",
    "editor.lineHighlightBorder": "#273136",
    "editor.lineHighlightBackground": "#ffbf0015",
    "editor.selectionBackground": "#ffbf0040",
    "editor.inactiveSelectionBackground": "#ffbf0020",
    "editorGroupHeader.tabsBackground": "#273136",
    "editorGroupHeader.border": "#1d2528",
    "editorWidget.background": "#1d2528",
    "editorHoverWidget.background": "#383f42",
    "editorHoverWidget.border": "#ffbf0060",
    "tab.inactiveBackground": "#1d2528",
    "tab.activeBackground": "#273136",
    "tab.activeBorder": "#fed96b",
    "tab.hoverBackground": "#273136",
    "tab.border": "#ffbf0060",
    "sideBar.border": "#161b1e",
    "sideBar.background": "#1d2528",
    "sideBarSectionHeader.background": "#161b1ea1",
    "panel.border": "#ffbf0060",
    "statusBar.background": "#1d2528",
    "titleBar.activeBackground": "#1d2528",
    "titleBar.border": "#ffbf0060",
    "activityBar.background": "#161b1e",
    "activityBar.foreground": "#fed96b",
    "tree.indentGuidesStroke": "#fed96b",
    "menu.background": "#273136",
    "menu.selectionBackground": "#ffbf0060",
    "debugToolBar.background": "#1d2528",
    "input.background": "#273136",
    "terminal.selectionBackground": "#ffbf0020"
  }
}
```

## Theme par default

```json
{
  "workbench.colorTheme": "Monokai"
}
```

## Customisation des couleur dans l'editeur

```json
{
  "editor.tokenColorCustomizations": {
    "textMateRules": [
      {
        "name": "Types for typescript",
        "scope": ["entity.name.type"],
        "settings": {
          "foreground": "#A6E22E",
          "fontStyle": "underline"
        }
      },
      {
        "name": "Import export return ES6",
        "scope": [
          "keyword.control.import",
          "keyword.control.export",
          "keyword.control.from",
          "keyword.control.flow",
          "keyword.control.default",
          "keyword.operator.assignment",
          "keyword.operator.type.annotation",
          "keyword.operator.type"
        ],
        "settings": {
          "foreground": "#F92672"
        }
      },
      {
        "name": "Type typescript",
        "scope": [
          "storage.type.type",
          "support.type.primitive",
          "storage.type",
          "support.class.component",
          "entity.name.type",
          "meta.type.paren.cover"
        ],
        "settings": {
          "foreground": "#66D9EF",
          "fontStyle": "italic"
        }
      },
      {
        "name": "Function params",
        "scope": [
          "variable.parameter",
          "meta.parameter.object-binding-pattern"
        ],
        "settings": {
          "foreground": "#FD971F",
          "fontStyle": "italic"
        }
      },
      {
        "name": "String",
        "scope": ["string.quoted.single", "string.quoted.double"],
        "settings": {
          "foreground": "#E6DB74"
        }
      },
      {
        "name": "Constant object key function name",
        "scope": [
          "variable.object.property",
          "entity.name.function",
          "variable.other.readwrite.alias",
          "variable.other.property",
          "punctuation.definition.tag.begin"
        ],
        "settings": {
          "foreground": "#F8F8F2"
        }
      },
      {
        "name": "Number",
        "scope": ["constant.numeric.decimal"],
        "settings": {
          "foreground": "#AE81FF"
        }
      },
      {
        "scope": ["entity.name.type"],
        "settings": {
          "foreground": "#A6E22E",
          "fontStyle": "underline"
        }
      }
    ]
  }
}
```
