# Go Wiki

A simple HTTP server rendering Markdown styled documents on the fly and optionally shows its git history including diffs.

**Warning** This is toy project to help me learn Go, so don't run this on anything exposed on the internet.

## Usage

Create git repository containing your Markdown formatted wiki pages.

### On the server

Create an empty repository.

``` bash
$ mkdir -p ~/www/wiki && cd $_
$ git init
$ git config core.worktree ~/www/wiki
$ git config receive.denycurrentbranch ignore
```

Setup a post-receive hook.

``` bash
$ cat > .git/hooks/post-receive <<EOF
#!/bin/sh
git checkout --force
EOF
$ chmod +x .git/hooks/post-receive
```

Start the go-wiki server.

``` bash
$ go-wiki --dir ~/www/wiki
```

### On your local machine

Replace `<user>` and `<host>` with credentials for your specific machine.

``` bash
$ git init
$ git remote add origin ssh://<user>@<host>/home/<user>/www/wiki
```

Now create some Markdown file and push.

``` bash
$ git add index.md
$ git commit -m 'Add index page'
$ git push origin master
```
