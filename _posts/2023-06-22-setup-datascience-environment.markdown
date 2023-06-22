---
layout: post
title: "How to Set Up a Data Science Environment in 5 minutes"
date: 2023-06-22 12:00:00 +0000
categories: python data guide
---
One of the key steps to any data science project is getting yourself set up with a well organised environment. Many guides start by just pip installing all the required dependencies and leave the reader to sort out the complete mess this leaves of your global python environment. 

Here I will show how to start every analysis / data science project.

The advantages of this system are myriad. The main one though is that you will be able to run all the notebook code, scripts and any future packages from within the same virtural environment.

My recommendation is to run this through [vs code](https://code.visualstudio.com/). This offers, in my opinion, the best developer experience for jupyter notebooks as well as allowing seamless transition into script, library, web app development. To get started just install the standard [Python Extension](https://code.visualstudio.com/docs/languages/python). 

## Project Set Up

Assuming you wish to track this project through git and github the first step is to start a new repo on GitHub with whatever name you wish. Be sure to initialise with a README, `.gitignore` and all the standard settings.

Clone this repo to your favourite directory (or the one that is most convenient).

Install [Poetry](https://python-poetry.org/).

Run `poetry init`. You will be confronted with a series of settings. These are not hugely important as they just determine what your `pyproject.toml` file will look like and that can be editted at any time.

I usually just skip through them and forget. 

Use `poetry add` to add any packages that you will need. The standard data science packages can be installed with `poetry add pandas numpy matplotlib seaborn scipy statsmodels ipykernel jupyter`. It is very important at this stage to install `ipykernel`. As this is crucial to the next and most important step.

Run `poetry run python -m ipykernel install --user --name {PROJECT_NAME}` This will give you a python kernel which can be used in your jupyter environment. It will be selectable from the drop down at the top right. In VS Code you can choose "Select Kernel" and then "Python Environments" and the env will exist in the sub list "Poetry Env". 

Now when you run code in the notebook it will be run inside the poetry managed virtual environment. This virtual environment can be played around with as much as you want. It can also be used to run any scripts or libraries you have in the project as well without impacting any other projects by installing new versions of packages etc. 

If you have a project for building finacial models you might need certain packages which you don't need for your fantasy football predictor project. Using poetry will allow you to keep them separate and stop you from bricking old projects when you start a new one. 

Poetry also allows you to add scripts at the project level. This can be useful for pulling latest datasets as in the example below.

Add a new directory called `scripts` and create a new file within called `load`. Into that file put the following:
{% highlight python %}
import pandas as pd

def data():
    df = pd.read_csv('https://https://example.com/data.csv')
    df.to_csv('data/dataset.csv', index=False)
    print("Latest dataset loaded to data/dataset.csv")

{% endhighlight %}

Next add this line to the `pyproject.toml`.

{% highlight toml %}
[tool.poetry.scripts]
load = "scripts.load:data"
{% endhighlight %}

Now when you run `poetry run load` the csv will be loaded into your `data` directory.

This gives you a rock solid position to start running new data science projects and you are ready to take them in any direction with very little effort. If your analysis leads you to need a python package, it is ready  to go. This is exactly how my [`invest-tools`](https://github.com/leo-jp-edwards/invest-tools) project started. Scaling to a full python package was easy from the position I had started from.

If you have any questions or issues please reach out. I am available through github :)