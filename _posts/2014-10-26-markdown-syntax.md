---
title: Markdown syntax introduction
modified: 2014-26-10
tags: [markdown, syntax, blogging, HTML]
excerpt: Plain text formatting syntax designed so that it optionally can be converted to HTML using a tool by the same name
lang: en
ref: markdown
---

### What is it?

Markdown is a **plain text formatting syntax designed so that it optionally can be converted to HTML using a tool by the same name**. Markdown is popularly used to format readme files, for writing messages in online discussion forums or in text editors for the quick creation of rich text documents.

Thus, “Markdown” is two things: (1) a plain text formatting syntax; and (2) a software tool, written in Perl, that converts the plain text formatting to HTML. 
The overriding design goal for Markdown’s formatting syntax is to make it as readable as possible. The idea is that a Markdown-formatted document should be publishable as-is, as plain text, without looking like it’s been marked up with tags or formatting instructions. While Markdown’s syntax has been influenced by several existing text-to-HTML filters — including Setext, atx, Textile, reStructuredText, Grutatext, and EtText, the single biggest source of inspiration for Markdown’s syntax is the format of plain text email.Markdown’s syntax is intended for one purpose: to be used as a format for writing for the web.

**Markdown is not a replacement for HTML**, or even close to it. Its syntax is very small, corresponding only to a very small subset of HTML tags. The idea is not to create a syntax that makes it easier to insert HTML tags. The idea for Markdown is to make it easy to read, write, and edit prose. HTML is a publishing format; Markdown is a writing format. Thus, Markdown’s formatting syntax only addresses issues that can be conveyed in plain text.
{: .notice}

### Iniline HTML

For any markup that is not covered by Markdown’s syntax, you simply use HTML itself. There’s no need to preface it or delimit it to indicate that you’re switching from Markdown to HTML; you just use the tags.
The only restrictions are that block-level HTML elements — e.g.` <div>,<table>, <pre>, <p>`, etc. — must be separated from surrounding content by blank lines, and the start and end tags of the block should not be indented with tabs or spaces. Markdown is smart enough not to add extra (unwanted) `<p>` tags around HTML block-level tags.

### Some history

The Markdown language was created in 2004 by John Gruber with substantial contributions from Aaron Swartz, with the goal of allowing people “to write using an easy-to-read, easy-to-write plain text format, and optionally convert it to structurally valid XHTML (or HTML)”. Gruber wrote a Perl script, Markdown.pl, which converts marked-up text input to valid, well-formed XHTML or HTML. Markdown has since been re-implemented by others as a Perl module available on CPAN (Text::Markdown), and in a variety of other programming languages. It is distributed under a BSD-style license and is included with, or available as a plugin for, several content-management systems.
Sites such as GitHub, reddit, Diaspora, Stack Exchange, OpenStreetMap, and SourceForge use variants of Markdown to facilitate discussion between users.

### Editors

While Markdown is a minimal markup language and is easily read and edited with a normal text editor, there are specially designed editors that preview the files with styles. There are a variety of such editors available for all major platforms; one such graphical editor for Windows is [MarkdownPad](http://markdownpad.com/). There are syntax highlighting plugins for Markdown built into emacs, gedit, and vim.
There are also online potions such us [Dingus](http://daringfireball.net/projects/markdown/dingus) and [StackEdit](https://stackedit.io/).

### Examples

The best way to understand markdown is to see it in use, here we can see a left column with the Markdown input and right column with the HTML output:

#### Headers
{% highlight css %}
A First Level Header
====================
A Second Level Header
---------------------
### Another deeper heading
{% endhighlight %}

{% highlight css %}
<h1>A First Level Header</h1>

<h2>A Second Level Header</h2>

<h3>Another deeper heading</h3>
{% endhighlight %}

#### Paragraphs
{% highlight css %}
Paragraphs are separated
by a blank line.
 
Let 2 spaces at the end of a line to do a  line break
{% endhighlight %}

{% highlight css %}
<p>Paragraphs are separated
by a blank line.</p>
 
<p>Let 2 spaces at the end of a line to do a<br />
line break</p>
{% endhighlight %}

#### Blockquote
{% highlight css %}
> This is a blockquote.
> 
> This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote
{% endhighlight %}

{% highlight css %}
<blockquote>
    <p>This is a blockquote.</p>

    <p>This is the second paragraph in the blockquote.</p>

    <h2>This is an H2 in a blockquote</h2>
</blockquote>
{% endhighlight %}

#### Emphasize
{% highlight css %}
Some of these words *are emphasized*.
Some of these words _are emphasized also_.

Use two asterisks for **strong emphasis**.
Or, if you prefer, __use two underscores instead__.
{% endhighlight %}

{% highlight css %}
<p>Some of these words <em>are emphasized</em>.
Some of these words <em>are emphasized also</em>.</p>

<p>Use two asterisks for <strong>strong emphasis</strong>.
Or, if you prefer, <strong>use two underscores instead</strong>.</p>
{% endhighlight %}

#### Links
{% highlight css %}
A [link](http://example.com).
This is an [example link](http://example.com/ "With a Title").
{% endhighlight %}

{% highlight css %}
<p>A <a href="http://example.com">link</a>.</p>
<p>This is an <a href="http://example.com/" title="With a Title"> example link</a>.</p>
{% endhighlight %}

#### Lists
{% highlight css %}
*   Candy.
*   Gum.
*   Booze.
(Unordered (bulleted) lists use asterisks, pluses, and hyphens (*, +, and -) as list markers)
1.  Red
2.  Green
3.  Blue

And if you have sub points, put two spaces before the dash or star:
Like this
And this
{% endhighlight %}

{% highlight css %}
<ul>
	<li>Candy.</li>
	<li>Gum.</li>
	<li>Booze.</li>
</ul>
<ol>
	<li>Red</li>
	<li>Green</li>
	<li>Blue</li>
</ol>  
<li>And if you have sub points, put two spaces before the dash or star:
	<ul>
		<li>Like this</li>
		<li>And this</li>
	</ul>
</li>
{% endhighlight %}

#### Reference
{% highlight css %}
I get 10 times more traffic from [Google][1] than from
[Yahoo][2] or [MSN][3].

[1]: http://google.com/        "Google"
[2]: http://search.yahoo.com/  "Yahoo Search"
[3]: http://search.msn.com/    "MSN Search"
{% endhighlight %}

{% highlight css %}
<p>I get 10 times more traffic from <a href="http://google.com/"
title="Google">Google</a> than from <a href="http://search.yahoo.com/"
title="Yahoo Search">Yahoo</a> or <a href="http://search.msn.com/"
title="MSN Search">MSN</a>.</p>
{% endhighlight %}

#### Image
{% highlight css %}
![alt text](/path/to/img.jpg "Title")
{% endhighlight %}

{% highlight css %}
<img src="/path/to/img.jpg" alt="alt text" title="Title" />
{% endhighlight %}