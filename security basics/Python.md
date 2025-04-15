
open content from console:
`import os; print(os.popen("ls -l").read())`

open content inside file:
`with open("app.py", "r") as f:
    print(f.read())
`

