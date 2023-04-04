#git

I used this [post](https://gist.github.com/Jonalogy/54091c98946cfe4f8cdab2bea79430f9) as base.

To generate the SSH key I followed this [Github Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)

The thin that was tripping me over was the remote url, we have to make sure that the url is the ssh format:

`url = git@github.com-user1:user1/your-repo-name.git`
