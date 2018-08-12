# expagem Specification

expagem ("Extensible Page Markup") is an easy to use HTML templating system. Here's how it works:

`say-hello.thtml` (Template)
```xml
<e-args>
  <arg name="person-name">Default Name</arg>
</e-args>
<e-template name="say-hello">
  <p>Hello, {person-name}!</p>
</e-template>
```

`example.ehtml` (Input)
```html
<html>

<head>
  <e-template path="./say-hello.thtml"/>
</head>

<body>
  <say-hello @person-name="Joe"/>
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

Template files end in `.thtml` and follow the syntax:

```xml
<e-args>
  <!-- Arguments go here -->
</e-args>
<e-template name="template-name">
  <!-- Template goes here -->
</e-template>
```

### Arguments

Denote arguments for the template inside the `e-args` section. If there are no arguments, you may omit this section.

In the body of the `e-args` section, list arguments for the template using the syntax:

```xml
<e-arg name="argument-name">Default Value</arg>
```

### Children

To insert the template's children in the template, use the `<e-children>` tag.

```html
<e-template name="template-name">
  <h1>Today's content</h1>
  <e-children>
  <small>&copy; Joe Schmoe</small>
</e-template>
```

### Template

Provide a `name` for the template. It is best practice to use the filename.

In the body of the `e-template` section, provide any HTML (zero or more tags). You must include the `e-template` section even if there are no HTML tags.

To substitute values in the HTML for the template's arguments, write the argument name surrounded in curly braces (`{` and `}`):

```html
<e-template name="favorite-color">
  <p>My favorite color is {color}.</p>
</e-template>
```
  
## Template usage

### Importing

You must use the `.ehtml` file extension to use expagem in your HTML. To "import" a template into your HTML, place the following syntax in the `<head>`:

```html
<e-template path="path/to/template.thtml"/>
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
