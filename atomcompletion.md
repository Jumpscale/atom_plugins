# Generate the docs for jumpscale
```
j.tools.objectinspector.generateDocs(dest='/tmp/tempd', objpath='j')
```
# Generated files in /tmp/tempd

```
In [3]: ls /tmp/tempd/
SUMMARY.md  compl.py  errors.md  jumpscale.api  out.pickled  j/
```

# the pickled api file stub file (out.pickled)

```
In [4]: cp /tmp/tempd/out.json /opt/out.pickled
```

# stubbing json api file 
You can generate a stub for jumpscale using this tool genjs8stub.py
https://raw.githubusercontent.com/xmonader/genjs8stub/master/genjs8stub.py

```
~ > python3 genjs8stub2.py /opt/out.pickled 

```
# using it from atom
	- go to the settings of autocomplete-python
	- add the path of the completion package for instance ~/compl to `Extra Paths for Packages`
or copy it to your dist-packages of the interpreter.

# using it from any other editor
You can use it from sublime/vscode or any other editor because it creates a valid python fake module.  
