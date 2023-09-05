A function can return true. 
```bash
true
echo $?

false
echo $?
```
Also returning false is possible all returns that are not zero are false

Example:
```bash
function check1()
{
   return 127
}

function check2()
{
   true
}

check1
echo $?

check2
echo $?

if check1; then echo "was true"; else echo "was false"; fi
if check2; then echo "was true"; else echo "was false"; fi
```
