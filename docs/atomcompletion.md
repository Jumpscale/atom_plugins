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

# stubbing pickled api file 

You should use : 
```j.tools.js8stub.generateStub(dest='/tmp/jscompl.py', pickledfile="/opt/out.pickled")```

# using it
copy the resulting python file to your dist-packages `should be under the name jscompl.py` and you will get a working code completion for your editor.
