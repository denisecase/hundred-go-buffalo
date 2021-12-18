# hundred-go-buffalo

## Background

- Read Go
- Read Buffalo
- Read [Getting Started on Heroku with Go](https://devcenter.heroku.com/articles/getting-started-with-go)

## Recommended Tools

- [PowerShell](https://microsoft.com/PowerShell) terminal
- [Chocolatey](https://chocolatey.org/) Windows package manager
- [VS Code](https://code.visualstudio.com/) for editing
- [Go / Golang](https://go.dev/) programming language
- [Buffalo](https://gobuffalo.io) - Golang web framework - with SQLite
- [Heroku]() - for deployment
- [Heroku PostgresQL]() - central datastore

## On Windows, Buffalo with SQLite Requires TDM-GCC

- Follow [Install Buffalo on Windows 10](https://blog.gobuffalo.io/install-buffalo-on-windows-10-e08b3aa304a3).

Then, open PowerShell as admin and install the rest. 

```PowerShell
choco install golang -y
choco install buffalo -y
choco install vscode -y
choco install heroku-cli -y
refreshenv
choco list --local
go version
go get -u -v -tags sqlite github.com/gobuffalo/cli/cmd/buffalo@latest
```
--------------

## Initial Generation Using buffalo new

```PowerShell
buffalo new hundred-go-buffalo
```

## CD and Open in Code for Editing

```PowerShell
cd hundred-go-buffalo
code .
```

- Add .gitignore. Ignore node_modules and files with secrets.
- Edit first line of go.mod to use github.com/username, e.g.: `module github.com/denisecase/hundred-go-buffalo`
- Add Procfile. 

## GitHub: Create Your Repo in the Cloud

In GitHub, create the repo to match. Create without adding any files.

## Heroku: Set up Deployment

```PowerShell
heroku login
```

Create a Herokup app. 

Add database. On the Heroku app dashboard, go to Resources / Add-ons / Heroku Postgres / Hobby Dev - Free.

Get all in one DATABASE_URL. On the Heroku app dashboard, go to Settings / Config vars / reveal to see DATABASE_URL.

Get DB vars. On the Heroku app dashboard, go to Resources / Heroku Postgres  / Settings / Database Credentials / View Credentials. Add these to your database.yml.

Configure autodeployment. On the Heroku app dashboard, go to Deploy / Set Deployment Method to GitHub / Set Connect to GitHub to username / repo (e.g., denisecase/) / Enable Automatic Deploys.

Monitor deployment. After deploying / on the app dashboard, go to Overview / click View Build Progress. 

- If successful, click "View App".
- If unsuccessful, click "More" / "View Logs".

## Database Setup

Copy database.yml-example to database.yml. Edit database.yml to use the correct usernames, passwords, hosts, etc... for your environment. I typically use only the central Heroku datastore, not a local one. 

Ensure that **you** start/install the database of your choice. Buffalo **won't** install and start it for you.

## Add Plugins

Add database pop plugin and auth plugin. 

```PowerShell
buffalo plugins install github.com/gobuffalo/buffalo-pop@latest
buffalo plugins install github.com/gobuffalo/buffalo-auth@latest
```

## Create Database

Ok, so you've edited the "database.yml" file and started your database, now Buffalo can create the databases in that file for you:

```PowerShell
buffalo pop create -a
```

## Generate Basic username / pwd Auth

Read [buffalo-auth](https://github.com/gobuffalo/buffalo-auth)

```PowerShell
buffalo generate auth
```

## Initial Commit

Open Powershell as Adminstrator in your repo folder on your local machine. 

```PowerShell
git init
git remote add origin https://github.com/denisecase/hundred-go-buffalo.git
git branch -M main
git add .
git commit -m "initial commit"
git push -u origin main
```

## Starting the Application

Buffalo ships with a command that will watch your application and automatically rebuild the Go binary and any assets for you. To do that run the "buffalo dev" command:

	$ buffalo dev

If you point your browser to [http://127.0.0.1:3000](http://127.0.0.1:3000) you should see a "Welcome to Buffalo!" page.

**Congratulations!** You now have your Buffalo application up and running.

## Generate MVC for Things

```PowerShell
buffalo g resource thing name body:text
```

## View Routes

```PowerShell
buffalo task routes
```

## Heroku CLI

```PowerShell
heroku config -a hundred-go-buffalo
heroku open -a hundred-go-buffalo
heroku logs --tail -a hundred-go-buffalo
```

## Go Best Practices

```PowerShell
go mod tidy
go mod vendor
```

## What Next?

We recommend you heading over to [http://gobuffalo.io](http://gobuffalo.io) and reviewing all of the great documentation there.

Good luck!

[Powered by Buffalo](http://gobuffalo.io)
