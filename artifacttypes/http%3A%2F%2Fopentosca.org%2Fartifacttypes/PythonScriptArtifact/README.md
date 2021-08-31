### PythonScriptArtifact
ArtifactType used to implement TOSCA Operation via a single Python 3 script

### Usage:

Add a single python 3 script file as a file

### Example python file:

```python
#!/usr/bin/env python
import sys
import os

def parseParameterFromArgV(argv, parameter):
    result = None
    for arg in argv:
        if str(parameter) + '=' in arg:
            result = arg[arg.index(str(parameter) + "=") + len(parameter)+1:]
    return result

def printOutput(dict):
    for key in dict:
        print(str(key) + '=' + str(dict[key]))

def main(argv):
    port = parseParameterFromArgV(argv, "Port")
    rootpath = parseParameterFromArgV(argv, "Rootpath")

    os.system('export DEBIAN_FRONTEND=noninteractive && apt-get install -yq apache2')
    os.system('service apache2 stop')

    # Share Output via printing as the last lines
    printOutput({'Port': port, 'Rootpath' : rootpath, 'Version' : 'SOMEVERSION'})

if __name__ == "__main__":
   main(sys.argv[1:])
```