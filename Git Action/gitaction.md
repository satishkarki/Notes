# GitHub Actions

There are many documentations out there about GitHub Actions but  [GitHub Docs](https://docs.github.com/en/actions/get-started/understand-github-actions), caught my eye. Lets dive in headfirst to create workflows to build and test some punches and get punched in the face. 

## Workflows, Events and Jobs
Workflow is defined in a .yaml file under .github/workflows directory in a repository. A repository can have mutiple workflows. each performing different tasks. Workflows run when triggered by an event in your repository, or they can be triggered manually, or at a defined schedule.

Example: Whenever I push my local repo to github using this command `git push origin -u main`, workflow is triggered to build and deploy the website and publishes the changes in my website [Satish Karki](www.satishkarki.com).

An event is a specific activity in a repo that triggers a workflow run. Im my case `git push` command.



