Quickly find your GitHub repositories from [Alfred](http://www.alfredapp.com/).

Based on a fork of `edgarjs/alfred-github-repos`, but changed A LOT to suit my needs.

# What's different in this fork?

### Security

Uses the OSX keychain to store the Github auth token instead of writing it to a file on disk.

### Ruby version

Modifies `$PATH` before executing the script to potentially use a more recent ruby version. The one I want to use is at `/opt/rubies/2.3.3/bin/ruby`, so that's what's set by default as an example. If you don't have a ruby version there, your system ruby will still be used. To use a recent ruby version on your system, change `export PATH="/opt/rubies/2.3.3/bin:$PATH` to `export PATH="/path/to/your/ruby/bin:$PATH"` in the following three workflow objects:
- gh Script Filter
- the "/bin/bash Run Script" for gh-refresh
- the "/bin/bash Run Script" for gh-auth

### Search behaviour
- Only searches the names of repos that belong to you or your organizations.
- Does a fresh search every time (no repo list cache).
- Returns 10 results max (more isn't useful in Alfred anyway IMO).
- Sorts results by recent activity. For me, this improved relevance, since I'm more likely to be looking for a repo with more recent activity.

# Usage

This workflow searches among your public and private repositories (including organizations you belong to) and opens them on GitHub.

### Identify yourself

This workflow searches on github and within your public and private repositories (including organizations you belong to). So you need to provide an access token to make things easy.

To generate an access token, go to [create a new personal access token](https://github.com/settings/tokens/new). You can enter any description and it just need to be checked the `repo` and `public_repo` option (read private and public repositories).

![Howto create access token](help_create-accesstoken.png)

Then **copy the token** (as it will be visible only that time!), and authenticate in Alfred:

    gh-auth YOURTOKEN

This will store your token and you will be able to use the following commands:

### List and search repositories

Search your own repositories and those of organizations you belong to by *keyword*

    gh KEYWORD

### Update local cache

To reduce the number of calls to the GitHub API, the workflow caches your GitHub username and list of organizations you belong to. If any of this information changes, you'll need to rebuild your local cache with:

    gh-refresh

# License

This is released under the [MIT License](http://opensource.org/licenses/MIT).
