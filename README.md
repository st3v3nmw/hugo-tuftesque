# Hugo Tuftesque Theme

Hugo Tuftesque is a minimalistic blog-like theme for the static site generator [Hugo](https://gohugo.io) that
implements the [Tufte-CSS](https://github.com/edwardtufte/tufte-css) project.

This is a fork of the [Hugo Tufte Theme](https://github.com/slashformotion/hugo-tufte) with some QoL improvements especially on mobile devices.

I maintain this theme for use on [my personal website](https://www.stephenmwangi.com/). If you need a less opinionated version that stays true to the original fork, please check out [this theme](https://github.com/loikein/hugo-tufte).

## Quickstart

### Prerequisite: Hugo Extended

You'll need to install Hugo **Extended** to use this theme since it uses SCSS. Check [this page](https://gohugo.io/installation/) for installation instructions.

### For a new site

```console
$ hugo new site <your-site-name>
$ cd <your-site-name>/themes/
$ git clone https://github.com/st3v3nmw/hugo-tuftesque.git
```

Add `theme = 'hugo-tuftesque'` to your `config.toml` to let your site know to actually use _this_ theme, specifically.

Then run `hugo server -D` and open up [localhost:1313](http://localhost:1313/) or wherever it says in your browser.

### Adding content

```console
$ hugo new content content/blog/the-page-title.md
```

## Features

### Math

[Katex](https://katex.org/) or [MathJax](https://www.mathjax.org) renders LaTeX written inside of Markdown files. LaTeX can be written more or less as normal.

Some examples:
- This `$\frac{1}{2}$` will be rendered inline.
- A simple displayed equation: `$$f(x, y) := e^{x^2 - y^2}.$$`

There currently seems to be some weirdness with other environments,
such as the `aligned` environment (`align*` is not supported by katex). These environments will render provided
they are wrapped in `<p>` tags and blank lines. The snippet below should
render correctly:

```latex
Let $G$ be a finite group with exponent $2$.  Then every element is
an involution, hence for any $x$, $y$ in $G$ we have:

<p>
\begin{aligned}
  e &= (xy)^2  \\
  &=xyxy \implies \\
  y^{-1} &= xyx \implies \\
  y^{-1}x^{-1} &= xy,
\end{aligned}
</p>

establishing that $G$ is abelian.
```

### Site Parameters

The site specific parameters that this theme recognizes are:

- `subtitle` string: This is displayed under the main title.
- `description` string: This is displayed in the description meta tag.
- `showPoweredBy` boolean: if true, display a shoutout to Hugo and this theme in the footer.
- `copyrightHolder` string: Inserts the value in the default copyright notice.
- `license` string: Shows the license your content is licensed under e.g. "CC BY 4.0". Defaults to "All rights reserved".
- `math` boolean: Site wide kill switch for Latex support.
- `katex` boolean: if "katex" is set to true katex will be used to render LaTex, if not MathJax will be used instead. Defaults to `true`.

**_Socials_**

You can add links to your social profiles by using these parameters:

- `github`: string
- `gitlab`: string
- `bluesky`: string
- `twitter`: string
- `medium`: string
- `youtube`: string
- `patreon`: string
- `stackoverflow`: string
- `reddit`: string
- `linkedin`: string
- `instagram`: string
- `mastodon`: string
- `orcid`: string
- `googleScholar`: string

Please see [st3v3nmw.github.io/config.toml](https://github.com/st3v3nmw/st3v3nmw.github.io/blob/main/config.toml) to see the full implementation with examples.

### Page Parameters

- `title` string: The page's title.
- `subtitle` string: The page's subtitle.
- `summary` string: The page's summary. It's displayed in the page's description meta tag.
- `draft` boolean: If `true`, do not display the page on production environments.
- `type` string: The page's type e.g. "post".
- `date` string: When the page was written.
- `math` boolean: If `true`, try to render the page's LaTeX code using MathJax.
- `meta` boolean: If `true`, display page metadata such as author, date, tags provided these page parameters exist and are not overridden. Pages of type "post" ignore this parameter and always display metadata.
- `toc` boolean: If `true`, display the table of contents for the page.
- `tags` / `categories` array[string]: The page's tags/categories.
- `hideDate` boolean: If `true`, do not display a page date. When `meta` is set to `true`, `hideDate` takes greater precedence.
- `hideReadTime` boolean: If `true`, do not display the page's reading time estimate.  When `meta` is set to `true`, `hideReadTime` takes greater precedence.

### Shortcodes

This theme provides the following shortcodes in an attempt to
support the features present in the
[Tufte-CSS](https://github.com/edwardtufte/tufte-css) project.

- `blockquote`
  - **Description**: Wrap text in a blockquote and insert optional
  `cite` or `footer` metadata.
  - **Usage**: Accepts the named parameters `cite` and `footer`.
  - **Example**:
  ```html
  {{<blockquote cite="www.shawnohare.com" footer="Shawn">}}
    There is nothing more beautiful than an elegant mathematical proof.
  {{</blockquote>}}
  ```

- `div`
   - **Description**: This shortcode is provided as a workaround for wrapping
   complex blocks of markdown in `div` tags. The wrapped text can
   include other shortcodes.
   - **Usage**: Identical to the `section` shortcode.
   Accepts the style parameters `class` and `id`.
   If only the positional argument `"end"` is passed, a closing tag
   will be inserted.
   - **Example**: `{{<div class="my-class">}}` inserts a
   `<div class="my-class">` tag, while
   `{{<div "end">}}` inserts the closing `</div>` tag.

- `epigraph`
  - **Description**: Create an epigraph with the wrapped text.
  - **Usage**: To include a footer with source attribution, pass in the
  optional named parameters `pre`, `cite`, `post`, `link`. These parameters
  make no styling assumptions, so spacing is important.  A more compactly
  styled epigraph will be used if the `type` parameter is set to `compact`.
  - **Example**:
  ```html
  {{< epigraph pre="Author Writer, " cite="Math is Fun" link='https://www.google.com' >}}
  This is an example of an epigraph with some math
  $ \mathbb N \subseteq \mathbb R $
  to start the beginning of a section.
  {{< /epigraph >}}
  ```

- `marginnote`
  - **Description**: Wrap text to produce a numberless margin note.
  - Usage: `{{<marginnote>}}...{{</marginnote>}}`
  - **Example**:
  ```html
  {{<marginnote>}}Some margin note{{</marginnote>}}
  ```

- `section`
   - **Description**: This shortcode is provided as a work-around for wrapping
   complex blocks of markdown in section tags. The wrapped text can
   include other shortcodes
   - **Usage**: Accepts the style parameters `class` and `id`.
   If only the positional argument `"end"` is passed, a closing tag
   will be inserted.
   - **Example**: `{{<section class="my-class">}}` inserts a
   `<section class="my-class">` tag, while
   `{{<section "end">}}` inserts the closing `</section>` tag.


- `sidenote`
  - **Description**: Wrap text to produce an automatically numbered sidenote.
  - **Usage**: identical to `marginnote`
  `{{<sidenote>}}...{{</sidenote>}}`
  - **Example**:
  ```html
  {{<sidenote>}}Some sidenote{{</sidenote>}}
  ```

### Icons

Icons are provided by the [Font Awesome](https://fontawesome.com/icons) project.
