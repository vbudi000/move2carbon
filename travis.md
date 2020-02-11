## Travis-ci

Travis-ci is used to automate integration action from a GIT repository change. As such it is very appropriate to use Travis to automatically rebuild the gh-pages branch from Gatsby every time the master branch changed. You must register the organization and repo in Travis-ci site https://travis-ci.com. 

To make a repository invoke travis-ci, create a file called `.travis.yml` in the root of your repository.
This is the content of the file to invoke gatsby build:


```
language: node_js
before_script:
  - npm install gh-pages --save-dev
  - git config --global user.name "gituser"
  - git config --global user.email "gituser@site.com"
  - echo -e "machine github.com\n  login $CI_USER_TOKEN" > ~/.netrc
node_js:
  - "10"
deploy:
  provider: script
  script: npm run deploy
  on:
    branch: master
```

The environment variable `CI_USER_TOKEN` is injected usint the travis CLI (in mac use `brew install travis`). 

		travis env set CI_USER_TOKEN the-generated-token --private -r gituser/reponame

The token is retrieved from the Git **Settings** > **Developer Settings** > **Personal access token**. 

When the repo is changed (PR merged or a commit being pushed) then the travis action is invoked and the gh-pages is automatically built.
