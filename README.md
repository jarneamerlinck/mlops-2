# Create an automated pipeline using Github Actions
Good, our code looks a little bit better already. Improvements can always still be made, and you are very welcome to refactor this code further if you want.  
Continuously refactoring eachother's code is part of a good DevOps workflow and should be encouraged (even if you would be changing a more senior data scientist's code who might be teaching your class today and therefore might get insulted because you're implying that his code is still terrible...).

Let's shift our focus towards the next step now: creating an automated pipeline.

## Theory
What happens if new data comes in and we need to retrain our model? Do we manually run the preprocessing step, the training step, and the model inference step to create our new predictions? That doesn't sound very CI/CD to me...

Let's address this problem by creating a pipeline that will automatically run our entire workflow every time new data is added to our *data/raw* folder.  
We don't even need to leave the safe haven of Github to accomplish this. We can do exactly that by using Github's built in CI/CD tool called **Github Actions**.

Github Actions allow us to run automated workflows in a separate cloud environment in reaction to events on Github, such as data being pushed into a repository.
Github Actions are built around two core concepts: the **workflows** and the **actions**. The workflow files specify when we should do something, the actions specify what we should do.  
Workflow files should always be created under the .github/workflows directory and are in the form of .yml files.  
Custom actions should preferably be created under the .github/actions directory. This is not mandatory, but simply good practice.  

The workflow files themselves can be thought of as having three levels:
1. At the top level we have the **workflow** itself which will react to a specified Github event and provision a Github Virtual Machine for our workflow to run.
2. Below the workflows we have **jobs**, or the overall tasks that should happens when a workflow is ran. Each job will be ran in parallell in its separate container (but more on containers later).
3. Below the jobs we have **steps**, or the small tasks that sequentially need to happen for a job to be complete. It's inside these steps that we will specify which actions should be taken.

You can find the full Github Actions documentation here: https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions

## Exercises
1. Clone this repository into your own Github account by clicking the big green button on the top right named 'Use this template'.
2. I took the liberty of already starting our pipeline. It's a simple pipeline, so we can have everything happening within the same job in the same workflow file. It's up to you to complete the next steps so we also automatically run a train step which will retrain our model. Go to the workflow file, add your next steps, and commit them into a new branch. If you want to test the workflow in your new branch, make sure to add your branch at the top of the workflow file.
3. Clone your repository into your local machine, make a change to the data in the *data/raw* folder, and push your changes to your new branch in your github repository. Observe what happens in your merge request and on the 'actions' tab on github.
4. If your workflow works, you can merge your branch into the main one and remove your old branch safely.

If you don't know how to work on a new branch on your local machine, then follow the steps below:
```bash
# Same as before, clone the repository
git clone link_to_your_github_repository

# Checkout to the new branch in your github repository
git checkout --track origin/new_branch_name

# When you have finished merging your branch back into 'main', then don't forget to delete your local branch
git checkout main
git branch -D new_branch_name
```

## Next Up

When you're finished, you can see the solution in the next repository: https://github.com/LukasMahieuArinti/mlops-3

We will continue our exercises there.
