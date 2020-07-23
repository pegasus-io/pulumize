# pulumize

Recipes to build from source all of the components of pulumi

I usually run pulumi with the `TypeScript` language. I started this repo, as an experminent, to check what are the exact dependencies of the gobal stack I am using, when I work with Pulumi and `TypeScript`.

When I have a clear idea of those dependenices, I will then find if there is any proprietary underlying dependency.

If there are no proprietary dependency, I will then also build from source all dependencies, including the nodejs runtime and associated components : 
* until I have no dependency that is not built from source
* except the folowing compilers : C / C ++ / Golang, and a few dev utilities fro those languages (linux packages)
* except all that is in the Docker container with debian buster, I will start FROM.
* that container is the container i will run the build from source in, using drone ci
* after the build from source, I will install the built binaries in many other contianers, using many other linux distros, maybe even windows containers : this to test the pulumi features are fully operational (this is the real pulumi)



## Building from source the pulumi cli and the base pulumi SDK (what we use on our workstations)

* The first component to build from source is the pulumi CLI 
* When pulumi CLi ins installed on your machine, you have in `~/.pulumi/bin` : 

```bash
jbl@poste-devops-jbl-16gbram:~$ ls -allh ~/.pulumi/bin/
total 142M
drwx------ 2 jbl jbl 4.0K Jun 30 15:42 .
drwxr-xr-x 4 jbl jbl 4.0K Jun 30 15:44 ..
-rwxr-xr-x 1 jbl jbl  47M Jun 30 15:42 pulumi
-rwxr-xr-x 1 jbl jbl  245 Jun 30 15:42 pulumi-analyzer-policy
-rwxr-xr-x 1 jbl jbl 1.1K Jun 30 15:42 pulumi-analyzer-policy-python
-rwxr-xr-x 1 jbl jbl  17M Jun 30 15:42 pulumi-language-dotnet
-rwxr-xr-x 1 jbl jbl  45M Jun 30 15:42 pulumi-language-go
-rwxr-xr-x 1 jbl jbl  17M Jun 30 15:42 pulumi-language-nodejs
-rwxr-xr-x 1 jbl jbl  17M Jun 30 15:42 pulumi-language-python
-rw-r--r-- 1 jbl jbl 4.7K Jun 30 15:42 pulumi-language-python-exec
-rwxr-xr-x 1 jbl jbl  238 Jun 30 15:42 pulumi-resource-pulumi-nodejs
-rwxr-xr-x 1 jbl jbl  990 Jun 30 15:42 pulumi-resource-pulumi-python
jbl@poste-devops-jbl-16gbram:~$ ls -allh ~/.pulumi/
total 36K
drwxr-xr-x   4 jbl jbl 4.0K Jun 30 15:44 .
drwxr-xr-x 207 jbl jbl  16K Jul 23 09:41 ..
drwx------   2 jbl jbl 4.0K Jun 30 15:42 bin
-rw-------   1 jbl jbl   57 Jul  9 12:53 .cachedVersionInfo
-rw-------   1 jbl jbl  404 Jul  9 12:53 credentials.json
drwx------   2 jbl jbl 4.0K Jun 30 15:44 workspaces
jbl@poste-devops-jbl-16gbram:~$ 
```

* Those binaries are built rom source using the top `Makefile` in the https://github.com/pulumi/pulumi repo : 

![where is pulumi CLI build from source](https://github.com/Jean-Baptiste-Lasselle/for-fellow-developers/raw/master/docuementation/impr.ecrans/pulumi/PULUMI_BUILD_FROM_SOURCE_2020-07-23T08-03-47.559Z.png)
