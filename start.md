``` bash
#!/usr/bin/env bash
set -u
set -f
set -o pipefail
readonly SCRIPT_NAME="${0##*/}"

# DESC: verbose_print() the provided string if verbose mode is enabled
# ARGS: $@ (required): Passed through to pretty_print() function
# OUTS: None
function verbose_print() {
  if [[ -n ${verbose-} ]]; then
    printf "%s\n" "$@"
  fi
}

# DESC: 
# ARGS: $@ (required): 
# OUTS: None
function demo_function() {
  verbose_print "This verbose function is called to describe the use of verbose in the demo function"
  printf "%s\n" "Hi, demo_function in action!"
}

# DESC: Usage help
# ARGS: None
# OUTS: None
function script_usage() {
  cat << EOF
${SCRIPT_NAME}: Easy template for starting simple scripts with documentation.
Usage:
     -h|--help                  Displays this help
     -v|--verbose               Displays verbose output
     -d|--demo                  Call the demo function
EOF
}

# DESC: Parameter parser
# ARGS: $@ (optional): Arguments provided to the script
# OUTS: Variables indicating command-line parameters and options
function parse_params() {
  local param
  while [[ $# -gt 0 ]]; do
    param="$1"
    shift
    case $param in
      '-?' | -h | --help)
        script_usage
        exit 0
        ;;
     -v | --verbose)
        verbose=true
        ;;
     -d | --demo)
        demoflag=true
        ;;
     *)
        printf "%s %s\n" "Invalid parameter was provided:" $param 
        exit 126
        ;;
    esac
  done
}

# try to put it on the top of the script for easy modification.
# DESC: Main control flow
# ARGS: $@ (optional): Arguments provided to the script
# OUTS: None
function main() {
  parse_params "$@"
  #lock_init system
  # here add your own commands and functions!
  verbose_print "Show the verbose function!"
  [[ -n ${demoflag-} ]] && demo_function
  printf "%s\n" "Main Function!"
}

# Invoke main with args if not sourced
# Approach via: https://stackoverflow.com/a/28776166/8787985
if ! (return 0 2> /dev/null); then
  main "$@"
fi
```
