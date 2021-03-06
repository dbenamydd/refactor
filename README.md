# Refactor

This is a single tool for now but might grow to include more.

**This is pretty early, pretty rough software. Treat it as alpha quality and carefully check any edits it makes.**


## Update imports

This helps you move code around in a project. For example, if you have
```python
pkg1/
  mod1.py
    def func1():
    ...
pkg2/
  mod2.py
    from pkg1.mod1 import func1
    ...
```
and you want to move func1 to mod2.py, you'd move the code manually, and then from the top level dir run
```sh
python update_imports.py --move=pkg1.mod1.func1,pkg2.mod2.func1 --verbose
```

Relative imports must start with a `.`.

This works for moving packages, modules, and symbols. It can update relative imports, although will convert them to absolute imports in some cases. It only updates imports so can't automatically fix things if you `import foo.bar` and move/rename `foo`.

It may result in slightly messy imports, for example it may create a new `from` import as part of a move even if one already exists that it could have added to, so you may want to run an import prettifier after it's done, like https://github.com/miki725/importanize or https://github.com/timothycrosley/isort.


## Contributing

Developed with python 2.7 so far.

```
python setup.py develop  # install deps
python tests/test_update_imports.py  # run tests
```

PRs welcome!
