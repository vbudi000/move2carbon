# move2carbon

This repo documents changes that must be made to move an existing documentation repo into Carbon theme.

1. Prepare required files, all these files are available in this repo:

	- gatsby-browser.js
	- gatsby-config.js (probably change the `pathPrefix` to indicate the reponame)
	- package.json

2. Create and populate the src directory:

	- src/data: contains `nav-items.json` that defines the left navigation pane
	- src/images: style based images and icon (additional images can be loaded here)
	- src/styles: carbon css file - must be there
	- src/gatsby-theme-carbon: additional control files that you must modify to add the navigation functionality
	- src/pages: **ALL** source navigation pane should be under here, an index.* file should exists as the initial page

3. Install and prepare the node.js components:

	```bash
	cd reponame
	npm install
	npm install gh-pages --save-dev
	npm install sharp node-sass
	```

	Note: sharp and node-sass are needed to be installed separately if you are using Mac (automatic install failed for me)

4. Populate content, some restrictions:

	- Content must be formatted properly, no HTML tag should be without closing tag
	- All reference to local repo should be relative, cannot use `{{ site.github.url }}`
	- Path name cannot have a special character (ie `_` or `$` etc)
	- Variables must be properly quoted or escaped 

	For example, for the following files:

	```
	src
	└─ pages
	   ├─ index.md
	   └─ content
	      └─ integration
	         ├─ introduction.md
	         ├─ pre-reqs.md
	         ├─ roks.md
	         └─ onprem-online.md
	```
 
5. Build your nav-items.yaml - note that all md files will be created as a directory and index.html file:

	```yaml
	- title: Home
	  pages:
	    - path: /
	- title: CloudPak for Integration
	  pages:
	    - title: Introduction
	      path: content/integration/introduction/
	    - title: Pre-requisites
	      path: content/integration/pre-reqs/
	    - title: cp4i-on-roks
	      path: content/integration/roks/
	    - title: onprem-online
	      path: content/integration/onprem-online/
	```

