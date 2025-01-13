# META: GIT-CLONE-ORGANIZATION

## Folder Structure

```plaintext
/Users/jasonnathan/Repos/git-clone-organization
├── README.md
└── git_clone_org

1 directory, 2 files
```
## File: README.md

```md
Git Clone Organization
======================

A _simple_ tool to clone all the repos in an organization. Works with 2-factor auth by way of a [personal access token](https://github.com/settings/applications#personal-access-tokens).

### Usage
* Clone this repo.
* `./git_clone_org`

```

## File: git_clone_org
```js
#! /usr/local/bin/node

var exec = require('child_process').exec;
var readline = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout
});

function Cloner() {
  readline.question('Enter your organization name: ', this.onOrgName.bind(this));
};

Cloner.prototype.onOrgName = function(orgName) {
  this.orgName = orgName;
  readline.question('Where would you like the org cloned to? ', this.onPath.bind(this));
  readline.write(process.cwd());
}

Cloner.prototype.onPath = function(path) {
  this.path = path;
  readline.question('Enter your personal access token (https://github.com/settings/applications#personal-access-tokens): ', this.onAccessToken.bind(this));
}

Cloner.prototype.onAccessToken = function(accessToken) {
  readline.close();
  var _this = this;

  try {
    process.chdir(this.path);
  }
  catch(e) {
    process.stdout.write('chdir: ' + e);
    return 0;
  }

  var apiCmd = 'curl -sS -u ' + accessToken + ':x-oauth-basic https://api.github.com/orgs/' + this.orgName + '/repos';
  exec(apiCmd, function(error, stdout, stderr) {
    _this.repos = JSON.parse(stdout);
    if(_this.repos.length) {
      _this.cloneRepo(0);
    }
    else {
      process.stdout.write("No available repos.\n");
    }
  });
}

Cloner.prototype.cloneRepo = function(index) {
  var _this = this;
  var repo = _this.repos[index];
  process.stdout.write("Cloning " + repo.name + "\n");
  exec('git clone ' + repo.ssh_url, function(error, stdout, stderr) {
    if(error) process.stderr.write("Error cloning "  + repo.name + ": " + error + "\n");
    if(index < _this.repos.length - 1) _this.cloneRepo(index + 1);
  });
}

module.exports = new Cloner();
```

## Git Repository

```plaintext
origin	git@github.com:richgilbank/git-clone-organization.git (fetch)
origin	git@github.com:richgilbank/git-clone-organization.git (push)
```
