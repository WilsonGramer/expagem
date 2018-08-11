# expagem Specification

expagem ("Extensible Page Markup") is an easy to use HTML templating system. Here's how it works:

`say-hello.htmlt` (Template)
```xml
<args>
  <arg name="to" internal-name="person-name">Default Name</arg>
</args>
<template name="say-hello">
  <p>Hello, {person-name}!</p>
</template>
```

`example.htmle` (Input)
```html
<html>

<head>
  <expagem-template path="./say-hello.htmlt">
</head>

<body>
  <say-hello @to="Joe"/>
</body>

</html>
```

`example.html` (Output)
```html
<!DOCTYPE html>
<html>

<head></head>

<body>
  <p>Hello, Joe!</p>
</body>
  
</html>
```

## Template syntax

Template files end in `.htmlt` and follow the syntax:

```xml
<args>
  <!-- Arguments go here -->
</args>
<template name="template-name">
  <!-- Template goes here -->
</template>
```

### Arguments

Denote arguments for the template inside the `args` section. If there are no arguments, you may omit this section.

In the body of the `args` tag, list arguments for the template using the syntax:

```xml
<arg name="argument-name" internal-name="optional-internal-name">Default Value</arg>
```

If `internal-name` is provided, you must use it inside the `template` section instead of the `name`. (`name` will continue to be accessible by users of the template; this is useful when you want a verb as the user-facing name, for example.)

### Children

To insert the template's children in the template, use the `<t-children>` tag.

```html
<template name="template-name">
  <h1>Today's content</h1>
  <t-children>
  <small>&copy; Joe Schmoe</small>
</template>
```

### Template

Provide a `name` for the template. It is best practice to use the filename.

In the body of the `template` tag, provide any HTML (zero or more tags). You must include the `template` section even if there are no HTML tags.

To substitute values in the HTML for the template's arguments, write the argument name surrounded in curly braces (`{` and `}`).

## Template usage

### Importing

You must use the `.htmle` file extension to use expagem in the file. To "import" a template into your HTML, place the following syntax in the `<head>`:

```html
<expagem-template path="path/to/template.htmlt">
```

Paths resolve in the same way as the `src` attribute in `<script>`, `<img>`, etc.

### Using

Anywhere in the `<body>` of your HTML, add your template in HTML-style syntax, but precede each argument with `@`:

```html
<my-template @key="value"/>
```

You may use self-closing syntax if no children are provided. If you provide children, use the standard XML syntax:

```html
<my-template @key="value">
  <!-- Children go here -->
</my-template>
```

## Converting expagem files to regular HTML

First, install expagem:

```
$ npm install -g expagem
```

Then pass your source files to the program like so:

```
$ expagem src/ -o output/
```

Pass input files/directories, then pass the output directory after the `-o` flag.

> NOTE: expagem converts input directories recursively.

The resultant files will appear in the specified output folder.

# Contributing

expagem is currently just a specification, but work on an implementation will begin soon! If you'd like to contribute, feel free to submit a pull request.
