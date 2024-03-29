


# Developing Content

## Overview of Developing Content

This chapter will show you how to publish a Workspace on AnVIL using RStudio. Publishing Workspaces programmatically makes it easier to incorporate version control (e.g., using [git](https://git-scm.com/)) and ensures that all of your notebook files end up in the Workspace.

Much of the information in this section comes from the [AnVILPublish vignette](https://bioconductor.org/packages/release/bioc/vignettes/AnVILPublish/inst/doc/AnVILPublishIntro.html), which can serve as an additional reference.

### Before You Start

1. You need to set up [Billing](#account-setup-instructors). This includes your Google Billing Account and Terra Billing Project. Take note of your Terra Billing Project name.

1. Create your [first Workspace](#first-workspace). A first Workspace is needed to launch RStudio, but after that, all Workspaces can be made programmatically from within other Workspaces.

1. Launch RStudio using the Community-Maintained RStudio Environment. This requires you to be familiar with [RStudio on AnVIL](#starting-rstudio).

## Set Up AnVILPublish on AnVIL

### Install AnVILPublish

Install `AnVIL` and `AnVILPublish`. Don't worry about loading it for now. Tip: hover over the top-right corner of the box below to copy the code.


```r
BiocManager::install("AnVIL")
AnVIL::install("AnVILPublish")
```

### Install `notedown`

Next, navigate to the RStudio Terminal and install [`notedown`](https://github.com/aaren/notedown) using `pip3`. This module converts markdown documents into `.ipynb` notebooks.


```bash
pip3 install notedown
```

Return to the RStudio Console. RStudio doesn't automatically know where to look for `notedown`. Add the `notedown` installation to your RStudio PATH:


```r
# Add to PATH
existing_path <- Sys.getenv("PATH")
notedown_path <- "/home/rstudio/.local/bin"
Sys.setenv(PATH = paste(existing_path, notedown_path, sep = ":"))
```

Confirm that `notedown` is ready to use:


```r
# Confirm notedown is accessible
system2("notedown", "--version")
```

You should see the version number printed to the console:

<img src="resources/images/04_Developing_content_files/figure-html//1HHWg47Tg6miv_K7GNB6ZDTx-4Jc5IMl7APfFtD1Rqag_gdb96a00840_0_80.png" title="Output on the RStudio console. You should see the version number printed if notedown has been installed correctly." alt="Output on the RStudio console. You should see the version number printed if notedown has been installed correctly." width="480" />

## Create Workspace Structure

### Identify Your Repository

You need a folder with content to get started. In the next step, this will be the basic structure of your files:

```
AnVILPublishSkeleton
|-DESCRIPTION
|-LICENSE.md
|-NAMESPACE
|-README.md
|-vignettes
  |-Notebook_1.Rmd
```

"AnVILPublishSkeleton" is the name of the folder containing all of your information. The folder must contain a `DESCRIPTION` file, `NAMESPACE` file, and a `vignettes` directory with at least one `.Rmd` file. As you develop content, you might end up with many `.Rmd` notebooks inside the `vignettes` directory. We will practice with a basic set of files that are already set up for you on [GitHub](https://github.com/).

First, you should clone the [skeleton repository](https://github.com/avahoffman/AnVILPublishSkeleton).


```bash
git clone https://github.com/avahoffman/AnVILPublishSkeleton
```

You'll notice it contains a `DESCRIPTION` file, `NAMESPACE` file, and a `vignettes` directory with an `.Rmd` file.

<img src="resources/images/04_Developing_content_files/figure-html//1HHWg47Tg6miv_K7GNB6ZDTx-4Jc5IMl7APfFtD1Rqag_geb84bbba9a_2_38.png" title="RStudio screenshot showing the files present in the cloned AnVILPublishSkeleton repository." alt="RStudio screenshot showing the files present in the cloned AnVILPublishSkeleton repository." width="480" />

### Changing the `DESCRIPTION` File

Edit the information in `DESCRIPTION` but keep the structure the same.

1. `Package:` argument: This "package name" must match the name of the folder containing the `DESCRIPTION` and other files. In this case, it should be "AnVILPublishSkeleton".

<img src="resources/images/04_Developing_content_files/figure-html//1HHWg47Tg6miv_K7GNB6ZDTx-4Jc5IMl7APfFtD1Rqag_geb84bbba9a_2_8.png" title="File screenshot showing the `Package:` argument is AnVILPublishSkeleton." alt="File screenshot showing the `Package:` argument is AnVILPublishSkeleton." width="480" />

2. `Title:` argument: This will become the header for your Workspace's Dashboard.

<img src="resources/images/04_Developing_content_files/figure-html//1HHWg47Tg6miv_K7GNB6ZDTx-4Jc5IMl7APfFtD1Rqag_geb84bbba9a_2_14.png" title="File screenshot showing the `Title:` argument is 'Workspace title on the Dashboard'." alt="File screenshot showing the `Title:` argument is 'Workspace title on the Dashboard'." width="480" />

3. `Authors@R:` argument: Your author information and roles. At minimum, you should include a first name, family name, a role, and an email. You can add additional authors and roles as needed. See a more detailed guide to package metadata [here](https://r-pkgs.org/description.html#author). The most common roles are creator (`cre`), author (`aut`), and contributor (`ctb`), but there are [many more](https://www.loc.gov/marc/relators/relaterm.html) to choose from if none of these fit the bill.

```
Authors@R: 
    person(given = "Firstname",
           family = "Lastname",
           role = "cre",
           email = "firstnamelastname@gmail.com")
```

4. `Description:` argument: A several-sentence description of the project.

### Changing Other Files

Do not edit the `NAMESPACE` file. The `README.md` file and `.Rmd` file(s) will be discussed in more detail in [Update Dashboard].

### Create the Workspace

Use the `AnVILPublish::as_workspace()` function. Replace `<billing-project>` with the appropriate Terra Billing Project of your choosing. Replace `<My-Workspace>` with the Workspace name of your choosing.


```r
AnVILPublish::as_workspace(
  path = "/home/rstudio/AnVILPublishSkeleton", # directory containing DESCRIPTION file
  namespace = "<billing-project>", # Billing project
  name = "<My-Workspace>", # Actual Workspace name
  create = TRUE # Makes a *new* Workspace
)
```

You will see output in the console as the function converts the `.Rmd` to `.md`. You might get some warning messages, but make sure that the Workspace was created without error:

<img src="resources/images/04_Developing_content_files/figure-html//1HHWg47Tg6miv_K7GNB6ZDTx-4Jc5IMl7APfFtD1Rqag_geb84bbba9a_2_20.png" title="Code to create a new Workspace produces knitr output in the console." alt="Code to create a new Workspace produces knitr output in the console." width="480" />

<img src="resources/images/04_Developing_content_files/figure-html//1HHWg47Tg6miv_K7GNB6ZDTx-4Jc5IMl7APfFtD1Rqag_geb84bbba9a_2_26.png" title="Code to create a new Workspace produces knitr output in the console. You should not see any errors in the output." alt="Code to create a new Workspace produces knitr output in the console. You should not see any errors in the output." width="480" />

You should now see this new Workspace at [`https://anvil.terra.bio/#workspaces`](https://anvil.terra.bio/#workspaces).

<img src="resources/images/04_Developing_content_files/figure-html//1HHWg47Tg6miv_K7GNB6ZDTx-4Jc5IMl7APfFtD1Rqag_geb84bbba9a_2_32.png" title="After running AnVILPublish, you should see the newly created Workspace in https://anvil.terra.bio/#workspaces." alt="After running AnVILPublish, you should see the newly created Workspace in https://anvil.terra.bio/#workspaces." width="480" />

## Update Dashboard

Edit the `README.md` file to add more details to your Workspace Dashboard page. You will use the same function you used to create the Workspace as to update it, with a small change. Instead of `create = TRUE` you’ll now see an argument `update = TRUE`. **Be very careful to use the correct Workspace name** here, so you don’t accidentally overwrite the wrong Workspace.


```r
AnVILPublish::as_workspace(
  path = "/home/rstudio/AnVILPublishSkeleton", # directory containing DESCRIPTION file
  namespace = "<billing-project>", # Billing project
  name = "<My-Workspace>", # Actual Workspace name
  update = TRUE, # Updates the Workspace with your changes
  use_readme = TRUE # Use README file for Dashboard Description
)
```

You can also click the pencil button next to “ABOUT THE WORKSPACE” to edit the Dashboard manually, but these changes won’t show up later in GitHub. They will also be overwritten by other AnVILPublish updates.

## Post Jupyter Notebook

The `.Rmd` file contains your content. You can make many `.Rmd` files. These will get turned into `.ipynb` Jupyter Notebooks when you update using AnVILPublish. After you make changes to your `.Rmd` files, update the Workspace by running:


```r
AnVILPublish::as_workspace(
  path = "/home/rstudio/AnVILPublishSkeleton", # directory containing DESCRIPTION file
  namespace = "<billing-project>", # Billing project
  name = "<My-Workspace>", # Actual Workspace name
  update = TRUE, # Updates the Workspace with your changes
  use_readme = TRUE # Use README file for Dashboard Description
)
```

Note that this is the same code used to update the Workspace Dashboard. You can use this exact code to update your workspace any time you save changes in RStudio!

## Push Changes to GitHub

Hosting your course's code on GitHub will ensure that it is reproducible, easy to update, and robust to any tweaks you make. After cloning the skeleton repository, you will need to make a few changes to ensure your content ends up associated with your GitHub account. This means you own it and can make/save changes!

Briefly, you should:

1. Create a new repository on [GitHub](https://github.com/new). Don't add a `README.md`, `.gitignore`, or license.

1. Return to RStudio on AnVIL and Initialize your `.Rproj`.

1. [`add`](https://git-scm.com/docs/git-add/en) and [`commit`](https://git-scm.com/docs/git-commit) your changes on AnVIL.  

1. [`rename`](https://git-scm.com/docs/git-remote) and [`add`](https://git-scm.com/docs/git-remote) a new origin that points to the new repository you just created.

1. [`push`](https://git-scm.com/docs/git-push) your changes. Remember that you will need to use a [GitHub Personal Token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token) instead of your password.

Git can be challenging. Please reach out to our community network at [`help.anvilproject.org`](https://help.anvilproject.org/) for help.
