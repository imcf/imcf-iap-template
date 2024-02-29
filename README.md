# imcf-iap-template

## Getting started

Starting a new IAP project with a new repo. Here's the how-to.

## Add the link of this repo to your IAP roject

## Invite user(s) this project is destined for

- [Go to the *Manage -> Members* page of your project](https://git.scicore.unibas.ch/imcf/default-iap-repo/-/project_members) and click on *invite members*. Pick the *Reporter* role (*Guest* permissions are not sufficient to see private repositories such as ours)
- [More details here](https://docs.gitlab.com/ee/user/project/members/)

## Working with Notebooks
Working with notebooks present the specific difficulty that outputs are committed alongside the code in a hard to read text file. Please clear your notebook before committing. Here we use nbconvert to do this using the CLI. Checkout [this link](https://stackoverflow.com/questions/28908319/how-to-clear-jupyter-notebooks-output-in-all-cells-from-the-linux-terminal#47774393) for details on the next 2 methods.

### Using nbconvert manually
You can manually trigger a notebook cleaning by running the following command on your notebook:
`jupyter nbconvert --clear-output --inplace my_notebook.ipynb`
This will clean any output from your notebook and allow you to compare it with another one easily.
### Using nbconvert automatically
You can configure your git to automatically run nbconvert before any commit. This has the advantage of keeping your local file in the same state (outputs are not removed) as well as removing the need to think about it everytime. To do so:
- add this to your local *.git/config* or global *~/.gitconfig*:
```
[filter "strip-notebook-output"]
    clean = "jupyter nbconvert --ClearOutputPreprocessor.enabled=True --to=notebook --stdin --stdout --log-level=ERROR"
```
Then create a *.gitattributes* file in your directory with notebooks, with this content:

```
*.ipynb filter=strip-notebook-output
``` 
or simply [copy the one from this repo](https://git.scicore.unibas.ch/imcf/default-iap-repo/-/blob/main/.gitattributes?ref_type=heads)

## Using smart commits
