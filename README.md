# AProjectHasNoName

## Project idea

The F# compiler needs to get files passed in correct order for compilation, so that everything is declared before usage. 
There are some different opinions if this should be seen as a feature or as a limitation. This project won't settle this dispute, but it wants to make it easier for F# developers to maintain that order in fsproj files.

The idea is to create a dotnet core tool that uses the FSharp.Compiler.Service to find a valid file order. Since there may exist more than one valid order, the tool will write the order into the F# project file (the fsproj file). The user will then commit the fsproj into version control and build servers will use exactly the one committed version. In contrast to multi-pass compilers this will remain a step that is done explicitly by the programmer and there always needs to be at least one valid order. In this sense the tool and the fsproj are very similar to paket and the paket.lock file. 

### Algorithm

This depends a lot on how much information we get from the FSharp.Compiler.Service. But the following properties should hold:

* If the fsproj already contains a valid order then we don't touch it 
* If we need to change the order then we try to keep the original order as stable as possible.
* If we there are multiple possible orders then we take the first one and exit 
* There may be heuristics needed to prefer certain parts of the search tree. We may try to make it opionated and force good practices 
* If we can't find a valid order we report an error text that is easy to understand for the programmer 
* If we can't find a valid order we may suggest how to fix the issue 

## Tasks 

- find a name

## Maintainers

This project will be done mostly by newcomers to the F# OSS ecosystem. This is an explicit decision in order to get more people involved. Long time members of the F# OSS sphere will mentor and try to help if things get stuck. 

- @forki - Mentoring
