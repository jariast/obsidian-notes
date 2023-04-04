#git

I used this [post](https://gist.github.com/Jonalogy/54091c98946cfe4f8cdab2bea79430f9) as base.

To generate the SSH key I followed this [Github Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)

The thing that was tripping me over was the remote url, we have to make sure that the url is the ssh format:

`url = git@github.com-user1:user1/your-repo-name.git`


## Fixing commits with incorrect account:

```sh
#!/bin/sh
 
git filter-branch --env-filter '
 
OLD_EMAIL="your-old-email@example.com"
CORRECT_NAME="Your Correct Name"
CORRECT_EMAIL="your-correct-email@example.com"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

Change the variables and run the script, use 

```sh
chmod +x <fileName>
```

To change the permissions and then:

```sh
git push --force --tags origin 'refs/heads/*'
```

IMPORTANT: this will overwrite ALL the commits in the branch.