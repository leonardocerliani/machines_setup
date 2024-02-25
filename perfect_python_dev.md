# Shaping the perfect python notebook environment
(at least for me)

NB: subject to many changes as I find improvements


## Why
Once you have experience developing in R using Rmarkdown in Rstudio, everything else looks like a pale attempt to imitate perfection.

I understand that the prototypical python developer _should_ be a serious and rough guy who doesn't mind suffering and adapting to develop in notepad. Instead I believe that developing code is already burdening your brain enough (a very pleasant burden, I want to stress) that you should not worry about the quirks of a poor development environment. (One day I will get to Vim, I promise...)

After long experimentations with _many_ different environments, I found one that works for me. 

It is not as perfect as RStudio, but that's the closest I got to. If you have suggestions for improvements, you are more than welcome.

For scripts development, I find VS code great. It automatically detects local virtual environments (hereafter venv) and allows you to evaluate single lines and code selections.

For notebooks, I find VS code still a bit in its early stage: there can be confusion between evaluating lines/cells in the associated terminal or in the interactive viewer, and also plots and tables appear in the interactive viewer, rather than inline.

Importantly - _very_ importantantly for me - you cannot evaluate a single line/selection inside a code cell. 

To be fair, the (my) perfect python notebook development environment _did already exist_: it was in the beautiful Atom editor with the Hydrogen extension. However, sadly in 2022 the decision was taken to "sunset" it, so now it can be a real hassle to make it work.

The best alternative I found so far is jupyter _lab_ (not jupyter notebook)

## Setting up jupyter lab

### Setting up the virtual environment

I prefer to work in a venv. In this case you just need to 

```bash
# create the venv and install jupyter lab
python -m venv pjl_venv
source pjl_venv/bin/activate
pip install jupyter notebook jupyterlab

# then launch it with
jupyter lab
```

### Basic keybindings

- A : Add code cell above
- B : add code cell below
- D-D : Delete the code cell
- M : convert default code cell to markdown
- Shift + Enter : evaluate current cell


### Evaluating a code selection

They make it as hard as possible for you to do this, but there _is_ a way. Once you are in a cell and have selected some code, if you check the Run menu it will show _Run Selected Text or Current Line in Console_. Without a keyboard shortcut...

To enable a keyboard shortcut you can follow the instructions [here](https://stackoverflow.com/questions/56460834/how-to-run-a-single-line-or-selected-code-in-a-jupyter-notebook-or-jupyterlab-ce) or read further.

Go to `Settings > Settings Editor > JSON Settings Editor`, which will open the Advanced Settings Editor

Now you can add the following snippet as a new item to the shortcuts list:

```json
{
    "command": "notebook:run-in-console",
    "keys": [
        "Ctrl Shift Enter"
    ],
    "selector": ".jp-Notebook.jp-mod-editMode",
    "args": {}
},
```

the first part of the complete file should like like the following

<details><summary>toggle shortcuts</summary>

```json
{
    "shortcuts": [
        {
            "command": "notebook:run-in-console",
            "keys": [
                "Ctrl Shift Enter"
            ],
            "selector": ".jp-Notebook.jp-mod-editMode",
            "args": {}
        },
        {
            "command": "application:activate-next-tab",
            "keys": [
                "Ctrl Shift ]"
            ],
            "selector": "body",
            "args": {}
        },

```
</details>

<br>

Of course you can use any other shortcut is more convenient for you rather than `Ctrl+Shift+Enter`


### Why I like it

I must admit that it's quite a luxury to be able to install an entire web-based IDE using a single - and never failing, at least for me - pip install.

On top of that, being a web interface, you can install it on any remote server, ssh using port forwarding and have it in your own local browser. Not bad at all.

This is a _great_ plus with respect to RStudio server, whose installation can require (based on my experience) a lot of painful time (besides, it' unlikely that you want to install RStudio server on each one of your 1,000 remote machines...)

Since jupyterlab is installed via pip, you can just pip freeze you venv to a requirements file and then have exactly the same vevn with jupyterlab in your remote server (`pip install -r requirements.txt`)


### What could be improved (IMHO)
With respect to RMarkdown, here you need to
- find your way to a pretty hidden location in the settings
- learn a couple of keybindings 

Besides this, there is the fact that it is not pure text as RMarkdown, hence the necessity to learn the keybindings. Personally, I also like to see only text in front of me. But that's just me.

On the other hand, since the result is a regular .ipynb notebook, once you have it on githun it is properly rendered - which is not the case for RMarkdown

Another thing that is not ideal - but it's a tradeoff with the previous item - is the fact that it is not pure markdown, so if you want to post it e.g. as an article, you still need to convert it to markdown

```bash
jupyter nbconvert --to markdown YourNotebook.ipynb
```

You can also export to html, however one _big_ issue related to this is that you cannot have code folding in exported web page. (But maybe this will [change](https://stackoverflow.com/questions/33159518/collapse-cell-in-jupyter-notebook)?)







