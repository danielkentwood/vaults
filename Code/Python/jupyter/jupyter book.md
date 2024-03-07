mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
related:: [[Jupyter]]

Start by installing Jupyter-Book and gh-import

```bash
conda install -c conda-forge jupyter-book ghp-import
```

To create a template book (probably the easiest way to get started -- you can modify with your content later), use the following command (with an example book called Team_Book) from your the root folder of your git repo:

```bash
jupyter-book create Team_Book/
```

This will create a new folder in your root folder; this new folder contains example content files and two YAML files:
1. \_config.yml: This sets up how the book is built, rendered, etc.  
2. \_toc.yml: This specifies the content tree and outlines the table of contents for the sidebar

Before you build your book, you need to push all of your latest changes to the default branch (let's assume it is `main` here):

```bash
git add -A Team_Book
git commit -m "update book"
git push -u origin main
```

To build the book, run the following command from your root folder:

```bash
jupyter-book build Team_Book/
```

Assuming there are no errors with the build, you can [[Use ghp-import to publish edits to jupyter book]]. Run the following from your root folder:

```
ghp-import -n -p -f Team_Book/_build/html
```




