# Unity Starter Project

Empty project which should be forked to form new Unity projects. All of our raw project setup should exist here.

## Windows Unity Machine Setup

### Install Git

1. https://git-scm.com/download/win
2. Run installer
3. Optionally install SourceTree (handy GUI)
    1. https://www.sourcetreeapp.com/
4. Run this from a command prompt:
    1. `git config --global core.autocrlf false`

### Add Largefile Support to Git

1. Install largefiles
    1. https://git-lfs.github.com/
2. Run the following from a command prompt:
    1. `git lfs install`

### Install Unity

1. Currently we're using 5.6.0f3
2. Create an empty project on your machine (I recommend C:\Dev\Empty_Unity)
3. Configure cache server (out of scope here)

### Configure Unity Merging

1. Locate the Unity merge tool
    1. Should reside at C:\Program Files\Unity\Editor\Data\Tools\UnityYAMLMerge.exe
    2. Validate that path or find your latest Unity install
2. Find your .gitconfig file
    1. On Windows, should reside at C:\Users\\\<username\>\\.gitconfig
3. Add the following lines to the end of the file:

        [merge "unityyamlmerge"]
            name = Unity's YAML (scene/prefab) merger
            driver = 'C:\\Program Files\\Unity\\Editor\\Data\\Tools\\UnityYAMLMerge.exe' merge -p --force "%O" "%B" "%A" "%A"

---
#### A Note About Araxis

Unity's default configuration for using Araxis as a fallback tool for merging is broken on windows (unfortunately). At some point Araxis switched from slash (/) options to dash (-) options and never updated their documentation. In order to get Unity's mergetool to work with it properly, we have to update it. The file is called mergespecfile.txt and is located at Editor/Data/Tools in the Unity installation (e.g. C:\Program Files\Unity\Editor\Data\Tools\mergespecfile.txt). 

Find this line:
```
* use "%programs%\Araxis\Araxis Merge\compare.exe" /3 /a2 /wait /title1:"Other" /title2:"Base" /title3:"Local" "%l" "%b" "%r" "%d"
```

And replace it with this one:
```
* use "%programs%\Araxis\Araxis Merge\compare.exe" -3 -a2 -wait -title1:"Other" -title2:"Base" -title3:"Local" "%l" "%b" "%r" "%d"
```
