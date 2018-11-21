_In-depth discussion of [taskbutler milestone #5 - Milestone: Feature - Ubuntu package .deb](https://github.com/6uhrmittag/taskbutler/milestone/5)_

This milestone will be the most complex milestone in taskbutler's development so far. The goal is fairly simple:

``apt-get install taskbutler``

The advantages are pretty obvious:

- _taskbutler_ doesn't need its own update process
- the user dosn't need to know a bit about Python
- the userbase is larger
- I finally learn how launchpad.net works and what's inside these mysterious .deb files
- *``apt-get install taskbutler`` sounds extremely cool! :D *

drawbacks:

- looks like a pretty complex topic
- many decisions to make
- even more work

# [Research default paths -> linux fhs](https://github.com/6uhrmittag/taskbutler/issues/118)

I already started to implement this in the pypi package. All Operating Systems have their common paths to put files files in. 
Since I focus on a Linux package I'll focus on the Filesystem Hierarchy Standard (FHS).

> #### danger::Draft
>
> The text below is in progress.

## The Filesystem Hierarchy Standard (FHS)

> [outlines the set of requirements and guidelines for file and directory placement under the Linux operating system.](https://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/index.html)

[Most Linux distributions follow the Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#FHS_compliance) and so, it's a great resource to learn about Linux in general. I couln't find a simular document for Microsoft's Windows, [but there are a few common directories as well](https://en.wikipedia.org/wiki/Directory_structure).
Whith these documents it's fairly easy do decide there to put program-/configuration-/and temporary files.
But this leads to a few decisions and requirements:

- each file has to be evaluated by
    - content individuality -> _Does the content vary by user?_ -> placement in user home
    - content sensitivy/secrets _How is allowed to read/write the file?_ -> file permissions
    - volatility
        - -> _Is it only a temp/cache file?_ ->  placement in /tmp
    - content type
        - -> _Logfile?_ -> placement in /var/log
        - -> _Can the file get big?_ -> a large file that fills a partition can crash a system. It should be avoided, but placement in /tmp could prevent this.

- each file can only contain content of it's path's scope. E.g. a global configuration is not allowed to contain user specific secrets like an API key.
- the placement of each file should be somewhat final. Files inside e.g. `\etc\taskbutler\` can change it's location whithin this directory, but the directory itself 
shouldn't move after the package is public. This would lead to potential migration issues on the user's system.


Luckily [The Python Standard Library](https://docs.python.org/3/library/index.html) already thought of this and provides [`os.path`](https://docs.python.org/3/library/os.path.html#module-os.path) to access these common paths.

## Additional Resources
- [Debian documentation](https://www.debian.org/doc/index.en.html)
    - [Debian Packaging Tutorial](https://www.debian.org/doc/devel-manuals#packaging-tutorial)
    - [Debian New Maintainers' Guide](https://www.debian.org/doc/devel-manuals#maint-guide)

# [create .deb package](https://github.com/6uhrmittag/taskbutler/issues/123)

# [add autodeployment travis -> launchpad](https://github.com/6uhrmittag/taskbutler/issues/121)

# [add CLI tests to verifiy function](https://github.com/6uhrmittag/taskbutler/issues/117)

# [add testkitchen CI to verify multiple distributions](https://github.com/6uhrmittag/taskbutler/issues/120)

