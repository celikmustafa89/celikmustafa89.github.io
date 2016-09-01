[[
title: Extensions
tags: [configuration, usage]
]]

[TOC]

# PyKwiki Extensions

## MarkDown Extensions

### pykwiki.ext.post

{tpl:versionwarning}
version: 1.0
{endtpl}

This extension is not compatible with the `wikilink` markdown extension.

This extension syntax is:

    [[page<:optional property>]]

Assuming you have a post in `source` called `home.md` with `title` set to "Home", then the following MarkDown:

    :::text
    Here is a link to [[home]]

Generates the following HTML:

    <p>Here is a link to <a href="/home.html" class="postlink">Home</a></p>

Similar things can be achieved with `title`, `blurb`, `url`, and `description`:

    :::text
    This is a link to [[home]], known as [[home:title]], found at [[home:url]]
    [[home:blurb]]
    [[home:description]]

Will create:

    <p>This is a link to <a href="/home.html" class="postlink">Home</a>, known as Home, found at /home.html
       This is just an example post used for testing random junk.
       This is just an example post used for ...</p>

#### Post sections

<span class="text text-muted">New in version <strong>1.0.3</strong></span>

One of the more poweful features of the `post` markdown extension is the ability to include sections from other pages.

You can specify a page section with `{section:name}` and `{endsection}`. 

For example, in a page called `faqs.md`, you could add a section such as the following:

    ::: text
    {section:foo}
    # This is a section about foo
    
    To learn more about foo, see <a href="foo">Foo</a>.
    {endsection}

Then to include that section in another page:

    :::text
    Below is a section from the FAQs page:
    [[faqs:section:foo]]


### pykwiki.ext.tpl


This extension allows for templates to be included in your source files. See [[templates]] for examples.

The basic usage is:

    :::text    
    {tpl:template_name}
    key: value
    {endtpl}

The above code will attempt to render a Jinja2 template named `template_name.tpl` inside of your source directory. 

**Example**

If you have a template called `project.tpl` located in `base_path/source`, and it contains the following content:

    :::text
    # {{name}}
    * Description: {{description}}
    * url: [{{url}}]({{url}})

And you include the following in one of your `md` pages.

    :::text
    {tpl:project}
    name: Widget System
    description: A fun widget system for everyone!
    url: http://widgets.com
    {endtpl}

Then PyKwiki will render `project.tpl` with the data from `{tpl:project}` into the HTML, like so:

    <h1>Widget System</h1>
    <ul>
        <li>Description: A fun widget system for everyone!</li>
        <li>url: <a href="http://widgets.com">http://widgets.com</a></li>
    </ul>

### pykwiki.ext.uml

<span class="text text-muted">New in version <strong>1.0.8</strong></span>

This extension is powered by [Plant UML](http://plantuml.com) and 
requires [python-plantuml](https://github.com/dougn/python-plantuml)
to be installed. 

#### Installation

    sudo pip install plantuml

Then add `pykwiki.ext.uml` to your `config.yaml` `extensions` section.

**Example**

    :::text
    {uml}
    Alice -> Bob: Connection
    Bob -> Marge: Another connection
    note left: This is just a note
    {enduml}

The above produces the following HTML by default.

    :::html
    <img src="http://www.plantuml.com/plantuml/img/utBCoKnELT2rKt3AJx9ISCxFoqjDBidCp-C2ya72leb5wQbM2evv-IKPgKKAoGW50000"/>

**Live example**

{uml}
Alice -> Bob: Connection
Bob -> Marge: Another connection
note left: This is just a note
{enduml}

