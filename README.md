# Getting started

Use AsciiDoc with Material for MkDocs.

> [!IMPORTANT]
> This package is an early release. The API may change without notice, and stability is not guaranteed. Use in production environments is not recommended. Feedback and testing are welcome.

This MkDocs plugin replaces the MkDocs default Markdown processor with [Asciidoctor](https://asciidoctor.org/) for AsciiDoc files, allowing you to write documentation in AsciiDoc while keeping full compatibility with Material for MkDocs.

The plugin uses Asciidoctor to build and then adjusts the output it to match MkDocs conventions.
The plugin ships some CSS/JS/RB and optionally injects "edit this page" links for included AsciiDoc modules when `repo_url` and `edit_uri` are configured.

Supports hot reload on the development server for all AsciiDoc source files when writing.

Asciidoctor attributes can be injected via the `mkdocs.yml`.

## Using mkdocs-asciidoctor-backend

```bash
pip install mkdocs-asciidoctor-backend --upgrade --pre
```

### Installing Asciidoctor

This plugin requires [Asciidoctor](https://asciidoctor.org/) to be installed and accessible from the command line.

**Linux/macOS:**

```bash
gem install asciidoctor rouge
```

**Windows:**

1. Install Ruby using one of these methods:
   - [RubyInstaller](https://rubyinstaller.org/) (choose "Ruby+Devkit") - installs to `C:\Ruby34-x64\`
   - [Chocolatey](https://chocolatey.org/): `choco install ruby` - installs to `C:\tools\ruby34\`

2. Install Asciidoctor:
   ```cmd
   gem install asciidoctor rouge
   ```

3. Find where Ruby is installed:
   ```cmd
   where ruby
   ```

4. Configure the full path to `asciidoctor.bat` in your `mkdocs.yml`:
   ```yaml
   plugins:
     - asciidoctor_backend:
         # RubyInstaller:
         asciidoctor_cmd: "C:/Ruby34-x64/bin/asciidoctor.bat"
         # or Chocolatey:
         # asciidoctor_cmd: "C:/tools/ruby34/bin/asciidoctor.bat"
   ```
5. Build and serve
   ```
   python -m mkdocs build -f demo/mkdocs.yml -v
   python -m mkdocs serve --livereload -f demo/mkdocs.yml
   ```

> [!NOTE]
> On Windows, you must use the `.bat` extension and provide the full path. The path depends on your Ruby installation location (e.g., `C:/Ruby34-x64/bin/` or `C:/tools/ruby34/bin/`).

> [!TIP]
> **Troubleshooting:** If `asciidoctor.bat` is not in Ruby's bin directory, your gem configuration may have a custom `--bindir` setting. Check with `gem env` and look for the "EXECUTABLE DIRECTORY" or custom gem configuration. You can install to Ruby's bin directory explicitly:
> ```cmd
> gem install asciidoctor rouge --bindir C:/Ruby34-x64/bin
> ```
> (Replace the path with your actual Ruby bin directory from `where ruby`)

> [!IMPORTANT]
>
> - MkDocs expects docs source in a `docs/` folder. See [Strategy for including docs from repository root](https://github.com/mkdocs/mkdocs/discussions/3062) for further discussion.
> 
> - For larger doc sets, set up a `nav` element in the `mkdocs.yml`, and optionally a root `docs/index.adoc` file. See [nav](https://www.mkdocs.org/user-guide/configuration/#nav) for more details.
> 
> - Asciidoctor xrefs might require you to set `relfileprefix` either globally in `mkdocs.yml` or per section/assembly file.

The following example `mkdocs.yml` can be dropped into the root of an existing AsciiDoc project. 

```yaml
site_name: Example
repo_url: https://github.com/example/repo
repo_name: example-repo
edit_uri: edit/main/

theme:
  name: material
  features:
    - content.action.edit
    - content.code.annotate
    - content.code.copy
    - content.code.select
    - navigation.footer
    - navigation.top
    - navigation.tracking
    - palette.toggle
    - search.highlight
    - search.suggest
    - toc.follow
    - toc.sticky
  palette:
    - scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/toggle-switch-off-outline
        name: Switch to dark mode
    - scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/toggle-switch
        name: Switch to light mode

exclude_docs: |
  partials/**
  snippets/**
  modules/**

plugins:
  - search
  - asciidoctor_backend:
      edit_includes: true
      fail_on_error: false
      ignore_missing: true
      safe_mode: safe
      attributes:
        imagesdir: images
        showtitle: true
        sectanchors: true
        sectlinks: true
        icons: font
        idprefix: ""
        idseparator: "-"
        outfilesuffix: .html
        source-highlighter: rouge
```

A demo docs site is published here: https://aireilly.github.io/mkdocs-asciidoctor-backend/
