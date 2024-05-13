Update docsy as a theme folder

適用於原先安裝方式採用 [Option 2: Clone the Docsy theme](https://www.docsy.dev/docs/get-started/other-options/#option-2-clone-the-docsy-theme)

1. Download Docsy [v0.10.0.zip](https://github.com/google/docsy/releases/tag/v0.10.0)

Remove folder d:\Projects\docsy-example-standalone\themes\Docsy
Unzip v0.10.0.zip to d:\Projects\docsy-example-standalone\themes\Docsy

2. Get Docsy dependencies

cd themes/docsy
npm install

3. Remove node_modules from .gitignore file.

4. Commit node_modules/*.*