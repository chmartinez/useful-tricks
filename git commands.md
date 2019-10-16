A very cool git command that I used is `filter-branch`. Basically, it lets you rewrite the commit history of a particular branch with tons of flexibility. 
But, as Uncle Ben used to say: "with great power comes great mistakes" so, read the manual before using it.
In my particular case, I used it to fix the commit author I used in a personal repo (github.com/chmartinez/hache-design-system). Here's the code I used:

```

git filter-branch --commit-filter '
        if [ "$GIT_COMMITTER_NAME" = "christian" ];
        then
                GIT_COMMITTER_NAME="hache";
                GIT_AUTHOR_NAME="hache";
                GIT_COMMITTER_EMAIL="chmartinez35@gmail.com";
                GIT_AUTHOR_EMAIL="chmartinez35@gmail.com";
                git commit-tree "$@";
        else
                git commit-tree "$@";
        fi' HEAD

```
What I did was to search for all the commits were the committer's name was "christian" and re-write them with a new committer name and a new author's email. And that's it!
Thanks to @kanzure and its awesome gist: https://gist.github.com/kanzure/5558267
