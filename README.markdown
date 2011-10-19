# Chocolat Code Completion Support

There's three prongs to Chocolat's code completion:

1. Word completion: words that are found in the current document. This happens when you press `esc`.
2. Indexed completions: symbols that are found in the current document or project. This is provided by [diglett](http://github.com/fileability/diglett).
3. **Static completions:** completions that are *not* found in the current document or project. What this repo is all about.

Static completions are things like CSS properties, standard library function names, etc. Things that could appear in Chocolat's code completion menu, but can't be indexed out of the document/project by diglett.

Here's how it works:

### Structure

Each language gets its own directory. In that the directory are:

1. JSON files holding *curated* completions (for example, CSS property names have to be manually curated).
2. Ruby/Python scripts, that perform some kind of processing, and print out JSON files to stdout (for example, extracting PHP function names out of its XML documentation).

Languages may have two subdirectories:

1. **support**: Holds resources that *should* be commited into the repo, and that scripts can expect to exist.
2. **tmp**: To be used to store resources that shouldn't be commited into the repo. For example, resources that can be downloaded online by the script, but you don't want to download *each* time.

### JSON format

Each JSON file is an object literal, with the following keys:

...

The *items* key is an array of strings and/or object literals. In the case of strings, it simply holds the

### Compiling

A script, `compile.py` runs all the scripts, then takes all the JSON files and compiles them into 1 monolithic completions.json file to be used by Chocolat.
