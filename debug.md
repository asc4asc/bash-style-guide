DEBUG use this!
================
``` bash
bash -x ./mybrokenscript
```
``` bash
#!/usr/bin/env bash
[..irrelevant code..]
set -x
[..relevant code..]
set +x
[..irrelevant code..]
``` 
``` bash
debug_prompt () { read -p "[$BASH_SOURCE:$LINENO] $BASH_COMMAND?" _ ;}
[..irrelevant code..]
trap 'debug_prompt "$_"' DEBUG
[..relevant code..]
trap - DEBUG
[..irrelevant code..]
``` 
