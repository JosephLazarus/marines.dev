# This is Marine Coders website repo

We are a group of U.S. Marines who use code to improve the lives of our fellow Marines.

On our website we offer members links to opportunities (such as the USAF Platform One Residency Program and a free trial to Cloud Academy), as well as links to ongoing Marine Coders projects, special events, and learning resources. Resources include self guided courses for:
* Learning to code
* Agile and DevOps methodologies
* Web development, Mobile Development, Front End/Back End frameworks
* Platforms and infrastructure
* and [more!](https://marines.dev/learn/) 
We also provide a link to the DOD DevSecOps services page provided by the USAF.

## What We Do
* We build code to help Marines!
* We open source as much as possible [cio.gov](https://sourcecode.cio.gov/OSS/) [code.mil](https://code.mil)
* We are responsible users of existing open source code
* We help each other

## Have questions or want to join us?
Join us in our chat channel, [Marine Coders Chat](https://chat.il2.dsop.io/signup_user_complete/?id=p65oraj9b3ysjgbxac7o7bn6fr), or send an email to collin.chew@usmc.mil / andrew.hutcheon@usmc.mil.  We would love to hear from you!  

### Public domain

This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).

All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.

### How to work in open source?

Check out the following resource for contributing to Open Source projects!
https://opensource.guide/how-to-contribute/ 

### Marine Coders Docs

Documenation theme / boilerplate is created using [https://github.com/mkdocs/mkdocs](https://github.com/mkdocs/mkdocs) and [https://github.com/squidfunk/mkdocs-material](https://github.com/squidfunk/mkdocs-material) with a series of extensions.

## Build Requirments

Prior to installation and repository setup ensure you have a version of Python 3.x installed and is correctly configured to the path.

```shell
> git clone https://github.com/marinecoders/marines.dev.git
> pip install -r requirements.txt
> mkdocs serve
    INFO     -  Building documentation...
    INFO     -  Cleaning site directory
    INFO     -  Documentation built in x seconds
    INFO     -  [09:19:58] Watching paths for changes: 'docs', 'mkdocs.yml'
    INFO     -  [09:19:58] Serving on http://127.0.0.1:8000/
```

The mkdocs insiders is available inside our private repository, you will need to download and conduct a `pip install -e <folder>`

## Follow On Development Guides

To continue to built onto this boiler plate please follow MkDocs or MkDocs-Material Guides listed.

## Contributors

We are open to contributors please view [contributions.md](/CONTRIBUTIONS.md)

## Custom Plugin Modification: `plugin.py` From updatesAT

A modified version of the MkDocs Material **Social plugin** is included in this repo at:

overrides/material/plugins/social/plugin.py


### ✅ Why this exists

This file overrides the default plugin located at:

Lib/site-packages/material/plugins/social/plugin.py


It has been **patched** to avoid issues caused by upstream changes to the way Google Fonts are fetched.

### 🧨 The Problem

The original plugin attempted to download Google Fonts (e.g., `Roboto`) as `.zip` files from [fonts.google.com](https://fonts.google.com). However, Google **disabled downloading fonts via `.zip` URLs**, which led to the following error when building or serving the site:

**ERROR** 
RealGetContents raise BadZipFile("File is not a zip file") zipfile.BadZipFile: File is not a zip file


After disabling the download logic, another issue appeared due to **recursive fallback logic** not being properly terminated:

RecursionError: maximum recursion depth exceeded in comparison


### ✅ The Fix

Made two key changes:

1. **Disabled the call to** `_fetch_font_from_google_fonts()` to stop trying to fetch fonts from Google.
2. **Added a short-circuit in** `_resolve_font()` to avoid infinite recursion if the requested font style isn't available.

This prevents the site from crashing and allows it to build and serve successfully **without external font dependencies**.

---

### 🧩 Optional: Downloading Fonts Locally

If you want to **retain social card typography** while avoiding external font requests, you can **manually download the fonts** and place them where the plugin expects them.

#### ✅ Steps:

1. **Download Roboto Font**:
   - Visit [https://fonts.google.com/specimen/Roboto](https://fonts.google.com/specimen/Roboto)
   - Click **Download Family** to get a `.zip` file.
   - Extract the `.ttf` files.

2. **Locate Your Cache Directory**:
   The social plugin looks for fonts in: marines.dev\.cache\plugin\social\fonts\Roboto

   
3. **Copy the Fonts**:
Place the desired `.ttf` files (e.g., `Roboto-Regular.ttf`, `Roboto-Bold.ttf`, etc.) inside that folder.


#### Once placed correctly, your custom plugin will use these local fonts instead of trying to fetch them from Google.

*test
---





