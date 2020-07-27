# How To Run

### Making A Post

`makepost [post-name]`

### Viewing Posts

`viewposts`

### Adding Post

`./deploy`


And that's all!

### Bash Profile Fn

```
function makepost() {
  now=$(date +'%Y-%m-%d')-"$1".md
  touch $now
  cat template.md > $now
  mv $now content/post/
}

function viewpost() {
  cd content/post
}
```

### Deploy Script

```sh
#!/bin/sh

# If a command fails then the deploy stops
set -e

printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

# Build the project.
hugo -D 

cp -r public/* ../ryan-schachte-git

# Go To Public folder
cd ../ryan-schachte-git

# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site $(date)"
if [ -n "$*" ]; then
	msg="$*"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

```
