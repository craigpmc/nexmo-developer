# Config Driven Landing Pages on Nexmo Developer

## Introduction

Config driven landing pages allow you to create pages with the content you need quickly and painlessly. Each landing page is generated from a [YAML](https://yaml.org/start.html) file in `/config/landing_pages/`. The name of the YAML file should be the same name as the URL you want for the landing page. For example, if you want a PHP language landing page that can be accessed at `https://developer.nexmo.com/php` then you need to name your YAML file `php.yml`.  

The config file represents rows and columns on a website with pre-defined content blocks. You can design your landing page with the visual layout that best works for your information and use the pre-defined content blocks to give your content shape and design.

Let's explore the building of a config file and then we will detail each content block and the data it accepts.

## Building A Config File

Each config file represents the visual layout of a landing page, including the number of rows and the amount of columns in each row, along with the actual information in the landing page. A config file begins with `rows:` that designate the `key` name of `rows` and the colon is the demarcator between the `key` name and the `value`. Within a YAML file, to specify an array of data one uses the `-` before the `key` name. This is an important element of the config file, as the data of `rows` and `columns` are held in arrays. Thus, the following will produce a single row with two columns:

```yaml

rows:
  - columns:
    - width: 2
      entries:
    - entries:

```

A column can either begin with the keyword of `entries` or the `key: value` pair of `width: integer`. The `width` value specifies how much of the row you would like that column to fill. Width is designated as a number between 1-4. If you do not specify a `width` the layout will default to a dynamically rendered arrangement of each column taking up an equal amount of space. The `entries` keyword, unlike the `width` keyword is mandatory, so even if you specify a `width` value, you still must begin the next line with `entries`.

What about other layout possibilities? This is how you would define a layout of 2 rows with 3 columns in the first and 1 column in the second:

```yaml

rows:
  - columns:
    - width: 1
      entries:
    - width: 2
      entries:
    - width: 1
      entries:
  - columns:
    - entries:

```

At this point we are ready to detail each content block type and the data associated with it.

## Content Types

### Action Button

The `action_button` content block creates a clickable linked HTML button you can add to the landing page. The YAML config for an action button is the following:

```yaml

- type: action_button
    action_button:
      text: # Text for the button (i.e. "Click here!")
      url: # The URL for the button (i.e. "https://developer.nexmo.com")

```

The `action_button` also takes optional parameters. **You do not need to define these optional parameters, unless you want their value to be `true` or the non-default.**:

```yaml

type: # "secondary" or "primary", with "primary" being the default. 
large: # true or false, with false being the default.
center_button: # true or false, with false being the default.

```

### Call To Action

The `call_to_action` content block creates a specific layout of text with an icon. You might want to use the `call_to_action` to draw attention to a featured area of Nexmo Developer, like our Community page, for example. The `call_to_action` block requires the following parameters:

```yaml

- type: call_to_action
  call_to_action:
    title: # Title for the content (i.e. "SDKs and Tools")
    icon: 
      name: # Name of icon to use (i.e. "icon-design-tools")
      color: # Color of icon (i.e. "blue-dark")
    url: # Link the call to action directs to (i.e. "/community")

```

In addition, you can also specify an optional `subtitle` parameter that gives you the opportunity to provide more descriptive text for your call to action. (_Note: You can use markdown in the `subtitle` to further style the content_.) For example, the following would render with the "SDKs and Tools" text in bold:

```yaml

subtitle: "Our **SDKs and Tools** provide you with everything you need to get up and running."`

```

### Contact Support

The `contact_support` content block is a pre-defined set of information that takes no parameters. Once you add it to your config file, it will populate with information about getting in touch with Nexmo for support. To add it to your config file, you must only reference it:

```yaml

- type: contact_support

```

### GitHub Repo

The `github_repo` content block lets you reference a GitHub repository on your landing page. It will display the name of the repository, the language, the number of stars and number of forks. The block will link to the repository directly on GitHub. It requires the following parameters:

```yaml

- type: github_repo
  github_repo:
    repo_url: # Link to repository on GitHub
    github_repo_title: # Name of repository (i.e. "Nexmo REST API client for .NET")
    language: # Language of code in repository (i.e. "Ruby")

```

### Header

The `header` block provides you with the layout for the landing page header content. The content consists of a title, with an icon, and an optional subtitle. You can specify the required parameters as such:

```yaml

- type: header
  header:
    title: 
      text: # The header title text (i.e. "Welcome!")
    icon: 
      name: # Name of icon to use (i.e. "icon-star")
      color: # Color of icon (i.e. "yellow")

```

There are also optional parameters for the `header` content block. You do not need to specify values for these optional parameters. You do so only if you want them to be set to `true` or their non-default value:

```yaml

title:
  text: # Header title
  align: # Text alignment, default is left-aligned if not defined (i.e. "center")
subtitle:
  text: # Subtitle text (i.e. "Find out more by reading the following.")
  align: # Subtitle text alignment, default is left-aligned if not defined (i.e. "center")
  type: # "large" or "small", default is small if not defined

```

Lastly, like the `call_to_action` subtitle, the text in the `header` subtitle is also capable of rendering markdown content.

### HTML

The `HTML` content block provides you with a place to insert HTML code that does not fit any of the pre-defined content blocks. Perhaps you wish to design a custom feature for a specific landing page and its needs, then this would be the tool to do so with. It's only required parameter is `content`:

```yaml

- type: html
  html:
    content: # Put HTML here (i.e. "<h2>Custom tags</h2>")

```

### Join Slack

The `join_slack` content block is a pre-defined styled invitation to join the Nexmo community Slack. It takes no parameters.

```yaml

- type: join_slack

```

### Line Divider

The `line_divider` content block is a pre-defined rendered line that can be used to visually divide a page. It takes no parameters.

```yaml

- type: line_divider

```

### Linked Image

The `linked_image` content block provides you with a format for an image that is linked to a URL. It takes the following parameters:

```yaml

- type: linked_image
  linked_image:
    image: # Link to image
    url: # Link to URL
    alt_text: # Alternate text if image cannot be rendered

```

### Products

The `products` content block is a pre-defined listing of all of Nexmo's API products. It displays each one with links to tutorials, guides, building blocks and API reference. It takes no parameters.

```yaml

- type: products

```

### Section Header

The `section_header` content block is used to create a header for a new section of content on your landing page. It renders a title with an icon. It takes the following parameters:

```yaml

- type: section_header
  section_header:
    title: # Title text goes here (i.e. "This is my title!")
    icon:
      name: # Name of icon (i.e. "icon-app")
      color: # Color of icon (i.e. "yellow")

```

### Structured Text

The `structured_text` content block provides the styling for a block of text content that features a title with an icon and subsequent paragraps of text. The text `content` can render markdown formatting. It takes the following required parameters:

```yaml

- type: structured_text
  structured_text:
    header: # Header text (i.e. "Write for us!")
    icon:
      name: # Icon name (i.e. "icon-envelope")
      color: # Icon color (i.e. "blue")
    text:
      - content: # Text content here, including markdown formatting (i.e. "**Text** goes here")
        type: # "large" or "small"

```

You can specify as many `text` blocks as you would like. Each `text` block consists of `content` and `type`.

### Text

The `text` content block provides you a space to insert plain text into your landing page, including with markdown formatting. It is structured as follows:

```yaml

- type: text
  text:
    content: # Text goes here (i.e. "This is __my__ text")

```

### Tutorial

The `tutorial` content block lets you link to a tutorial and show a tutorial image, if one exists, and a tutorial title and description. The only parameter it requires is the `name` of the tutorial file on Nexmo Developer. The renderer will retrieve the rest of the details from the tutorial file itself:

```yaml

- type: tutorial
  tutorial:
    name: # Name of tutorial (i.e. mobile-app-invites)

```

### Unordered List

The `unordered_list` content block lets you create a list of items and specify the shape of the list bullet item demarcator. It accepts the following required parameters:

```yaml

- type: unordered_list
  unordered_list:
    list:
      - item: # First item in list
      - item: # Second item in list
      - item: # Third item in list
      - item: # Fourth item in list

```

As mentioned, you can also specify the shape of the list bullet with the `bullet_shape` parameter:

```yaml

bullet_shape: # Shape of bullet, if not defined it will default to a circle (i.e square)

```