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
function check()
{
   return 127
}
check
echo $?

check
if [[ check ]]; then echo "was true"; else echo "was false"; fi
```
