# Linux Relative Paths

```./``` : Current directory 

```../``` : One directory back

```~/``` : Users home directory

can be used with commands eg.ls ./

# Operators

```>``` : Sends output to file for anything ```eg. echo ff > example.txt``` replaces existing file

```>>``` : Appends to existing file ```eg. echo ff >> example.txt```

```&&``` : Execute the second command only, if the execution of first command succeeds.

```||``` : Execute second command only if the execution of first command fails.

```&``` : The function of & is to make the command run in background. Just type the command followed with a white space and &. You can execute more than one command in the background with ```eg. ls & whoami```

```$``` : Denotes system variable like $USER, $SHELL can be set with ```eg. export <varname>=<value>```

```|``` : Use output of one command as input to following command ```eg. ls -al | grep flag```

```;``` : The ; operator makes it possible to run, several commands in a single go and the execution of command occurs sequentially. ```eg. ls ; whoami ; mkdir temp```
