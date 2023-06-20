# Different credentials per repo

Sometimes you need to use different ssh/auth keys for github/gitlab/etc. Simple way to do it is to setup the `~/.ssh/config` file with different hosts. Liket his:

```
Host github.com-ls_github
    HostName github.com
    AddKeysToAgent yes
    User git
    IdentityFile ~/.ssh/id_rsa_ls_github
```

Then inside the repo the origin/remote URL has to be match the `Host` from config file, like this:

```
[remote "origin"]
url = git@github.com-ls_github:<repo ulr>.git
fetch = +refs/heads/*:refs/remotes/origin/*
```

Done!
