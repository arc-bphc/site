## Workflow guidelines 

To add your blogs to the repository, follow these steps. 

1. Just head over to the GitHub page and click the "Fork" button. Then clone your fork to your local machine using: 

   `git clone https://github.com/username/arc-bphc.github.io` 

2. Add upstream repo to list of remotes:

   `git remote add upstream https://github.com/arc-bphc/arc-bphc.github.io` 

3. Verify the remote:

   `git remote -v` 

4. When you want to update your fork with the latest changes: 

```
   git fetch upstream
   git checkout master
   git merge upstream/master
``` 

5. Since this is a relatively simple repository, you can work in the master branch of your fork instead of a separate branch. Add your post in the `_posts` folder in Markdown format with proper YAML values at the top, as in the sample post. 

6. Add all your changes and commit them in the master branch of your fork. 

``` 
    git add . #adds all changes at once 
    git commit -m "commit message" 
``` 

7. Push the changes. 

   `git push origin master` 

8. Go to the page of your forked repo and make a Pull Request from there.   
