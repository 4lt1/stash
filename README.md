Stash tools
===========

Go package of Stash tools

## Installation

```bash
make
```

## Usage

```bash
go get github.com/xoom/stash

import "github.com/xoom/stash"
```

### Stash Rest API Documentation

* [Rest APIs](https://developer.atlassian.com/stash/docs/latest/reference/rest-api.html)

### NewClient

```go
stashClient := stash.NewClient("stash_user", "stash_pwd", "http://stash-url.local:7990")
```

### CreateRepository

```go
repository, err := stashClient.CreateRepository("PROJ", "slug")
```

### GetRepositories

```go
repository, err := stashClient.GetRepository("PROJ", "slug")
```

### GetBranches

```go
branches, err := stashClient.GetBranches("PROJ", "slug")
```

### GetRepository

```go
repository, err := stashClient.GetRepository("PROJ", "slug")
```

### CreateBranchRestriction

```go
branchRestriction, err := stashClient.CreateBranchRestriction("PROJ", "slug", "develop", "user")
```

### GetBranchRestrictions

```go
branchRestrictions, err := stashClient.GetBranchRestrictions("PROJ", "slug")
```

### DeleteBranchRestriction

```go
err := stashClient.DeleteBranchRestriction("PROJ", "slug", branchRestriction.Id)
```

### GetPullRequests

```go
// get all pull requests
pullRequests, err := stashClient.GetPullRequests("PROJ", "slug", "")

// get pull request by state
state := "OPEN"
pullRequests, err := stashClient.GetPullRequests("PROJ", "slug", state)
```

### GetPullRequest

```go
// get pull request by id
pullRequest, err := stashClient.GetPullRequest("PROJ", "slug", 1)
```

### CreatePullRequest

```go
title     := "A Title"
des       := "A Description"
from      := "feature/file1"
to        := "develop"
reviewers := []string{"bob", "bill"}

pullRequest, err := stashClient.CreatePullRequest("PROJ", "slug", title, desc, from, to, reviewers)
```

### CreateComment

```go
comment, err := stashClient.CreateComment("PROJ", "slug", 1, "build passing")
```

### UpdatePullRequest

```go
title     := "New title"
desc      := "New description"
branch    := "master"

pullRequest, err := stashClient.UpdatePullRequest("PROJ", "slug", "1", 10, title, desc, branch, nil)
```

### GetRawFile

```go
filePath := "foo/bar"
branch   := "develop"

data, _ := stashClient.GetRawFile("PRJ", "slug", filePath, branch)

fmt.Println(string(data))
```

### stash

## Development

### Local stash instance

Download and run a development instance of stash via a
[docker image](https://www.docker.com/).

```bash
# pick a directory where to save the data generated by the container
export STASH_DATA="${HOME}/stash/data"

# for a linux host
$ docker run -u root -v $STASH_DATA:/var/atlassian/application-data/stash atlassian/stash chown -R daemon  /var/atlassian/application-data/stash

$ docker run -v $STASH_DATA:/var/atlassian/application-data/stash --name="stash" -d -p 7990:7990 -p 7999:7999 atlassian/stash

# for a MacOs Host via 'boot2docker'
$ docker run -u root -v $STASH_DATA:/var/atlassian/application-data/stash --name=stash -d -p 7990:7990 -p 7999:7999 atlassian/stash
```

Open your browser to `http://localhost:7990` and follow the setup instructions.

** If your are using boot2docker get your IP via `boot2docker ip`
