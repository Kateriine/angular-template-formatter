# Angular Template Formatter README

# ###DEPRECATED###

## This plugin is no longer maintained due to the impossibility to add Angular compiler module in commonjs.

Extension for formatting Angular 2+ HTML templates. This extension is opinionated and not very configurable.

## Install:

in .vscode/settings.json:

```
  "[html]": {
    "editor.defaultFormatter": "kateriine.kat-angular-template-formatter"
  },
```

## Formatting:

When run, this extension will put each HTML attribute on its own line—unless there is a single attribute declared on the HTML tag. In the case of a single attribute, the tag and attribute will be put on a single line.

## Example:

This template from the Angular [Tour of Heroes](https://github.com/johnpapa/angular-tour-of-heroes/blob/master/src/app/hero-search.component.html):

```html
<div id="search-component">
  <h4>Hero Search</h4>

  <input #searchBox id="search-box" (keyup)="search(searchBox.value)" />

  <div>
    <div
      *ngFor="let hero of heroes | async"
      (click)="gotoDetail(hero)"
      class="search-result"
    >
      {{hero.name}}
    </div>
  </div>
</div>
```

will get formatted to:

```html
<div id="search-component">
  <h4>Hero Search</h4>

  <input #searchBox id="search-box" (keyup)="search(searchBox.value)" />

  <div>
    <div
      *ngFor="let hero of heroes | async"
      (click)="gotoDetail(hero)"
      class="search-result"
    >
      {{hero.name}}
    </div>
  </div>
</div>
```

Svg prefixes will remain intact:

```html
<svg
  xmlns="http://www.w3.org/2000/svg"
  width="24"
  height="24"
  viewBox="0 0 24 24"
>
  <svg:path
    d="M20.5 6c-2.61.7-5.67 1-8.5 1s-5.89-.3-8.5-1L3 8c1.86.5 4 .83 6 1v13h2v-6h2v6h2V9c2-.17 4.14-.5 6-1l-.5-2zM12 6c1.1 0 2-.9 2-2s-.9-2-2-2-2 .9-2 2 .9 2 2 2z"
  />

  <svg:path fill="none" d="M0 0h24v24H0z" />
</svg>
```

Concat of element and text will stay on the same line so won't be visually separated by a fake space.

```html
<span>text</span>textnode<span>text</span>
won't become this
<span>text</span>
textnode
<span>text</span>
```

(Expected result):
<span>text</span>textnode<span>text</span>
won't become this
<span>text</span> textnode <span>text</span>

## Recommended Configuration:

```

{

// turn off default vs code formatter

"html.format.enable": false,

// enable formatting by default

"editor.formatOnSave": true,

"editor.formatOnPaste": true

}

```

## Release Notes

### 0.1.6

Allow space in text if there is no new line

### 0.1.5

Remove new lines (\n) before and after text nodes to prevent spaces added by browser

### 0.1.3

Svg prefixes are mantained (svg:path, svg:g ...)

### 0.1.2

Preserves HTML escaped entitities

### 0.1.1

Does not remove <!DOCTYPE> tags when formatting.

### 0.1.0

Now formats svgs in templates

### 0.0.8

Added option for preventing closing tag `>` from being on their own line: `kat-angular-template-formatter.closeTagSameLine`. Thanks @larscom!

### 0.0.7

Added an option for tabs vs spaces. Thanks @Empereol!

### 0.0.2

Added configuration option for indentWidth, defaults to 4.

### 0.0.1

Initial release of Angular template formatter
