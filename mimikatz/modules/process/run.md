# run

It creates a process by using the [CreateProcessAsUser](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessasusera) Win32 API function. The [CreateEnvironmentBlock](https://docs.microsoft.com/en-us/windows/win32/api/userenv/nf-userenv-createenvironmentblock) is also utilized. It has the following command line argument:

* positional argument: the name of the process to run

![Run notepad.exe](<../../../.gitbook/assets/1 (2).png>)
