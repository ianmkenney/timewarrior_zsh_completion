# timewarrior zsh completion

zsh completions for the timewarrior time tracking command line application.

## Usage

Copy or link the `_timew` file in a path under the `$fpath` array. 
If adding a new path for `fpath` in your `zshrc`, make sure to 

```
autoload -U compinit; compinit
```

after the change. Start a new session and completion should work.