Update docsy as a theme folder

適用於原先安裝方式採用 [Option 2: Clone the Docsy theme](https://www.docsy.dev/docs/get-started/other-options/#option-2-clone-the-docsy-theme)

1. Download Docsy [v0.10.0.zip](https://github.com/google/docsy/releases/tag/v0.10.0)

Remove folder d:\Projects\docsy-example-standalone\themes\Docsy
Unzip v0.10.0.zip to d:\Projects\docsy-example-standalone\themes\Docsy

2. Install node modules

```text
d:\Projects\docsy-example-standalone
npm install
npm install -D autoprefixer
npm install -D postcss-cli
npm install -D postcss
```

**Important:** Hugo may fail to build your website if autoprefixer is not installed. See: [Docsy issue #999](https://github.com/google/docsy/issues/999)

3. Remove `node_modules` from .gitignore file.

4. Commit node_modules/*.*

5. Download Font-Awesome souce code from GitHub and save to `/themes/FortAwesome/Font-Awesome` folder.
6. Download Bootstrap souce code from GitHub and save to `/themes/twbs/bootstrap` folder.
7. Edit `/themes/docsy/hugo.yaml`, modify path as below:

```yaml
  ....
  imports:
    # 2024-05-14 Michael: removed "github.com/"
    - path: twbs/bootstrap
      disable: false
      mounts:
        - source: scss
          target: assets/vendor/bootstrap/scss
        - source: dist/js
          target: assets/vendor/bootstrap/dist/js
    # 2024-05-14 Michael: removed "github.com/"
    - path: FortAwesome/Font-Awesome
      disable: false
      mounts:
        - source: scss
          target: assets/vendor/Font-Awesome/scss
        - source: webfonts
          target: static/webfonts
```

8. Fix Mermaid.JS loading error

Create a test markdown file and add a mermaid diagram in it. Then run `hugo server` command. If the command fails with the following error:

```text
Could not retrieve mermaid script from CDN.
Reason: error calling resources.GetRemote: 
  Get "https://cdn.jsdelivr.net/npm/mermaid@latest/dist/mermaid.esm.min.mjs":
    dial tcp 104.18.186.31:443: i/o timeout
```

It indicates that the mermaid JavaScript cannot be downloaded from your machine. It could be due to a firewall blocking it.

To fix the error, we can create a `mermaid.html` file to override the default one. To do this, create the file `mermaid.html` under /layout/partial/scripts/ folder, and paste the following content:

```html
<script type="module">
    import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid/+esm'
</script>    
```

Work done.