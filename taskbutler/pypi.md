---
description: Getting serious is hard.
---

# Publishing to pypi

Before I started developing Taskbutler, I had no idea how this magical `pip install xyz` workes. I'm still not a fan of `pip install`. It can be frustrating and confusing when using different computers and operating systems. Especially in the light of `apt-get install X; apt-get update; apt-get upgrade`.

But publishing a package on pypi(which is the main resource for `pip install`) marks a major milestone when experimenting with Python. Publishing a random script is easy. Publishing a somewhat pretty package which is usable by random people requires much more work:

- a readme (preferably in .rst and not .md)
- a working setup.py
- a test that verifies that the package is installable
- an idea about the required Python version
- a simple workflow that isn't annoying

Since most _production like tools_ requires the above anyway, I went on refactoring the code to meet the requirements. It took weeks to figure out what's needed and how to archive it. Even with so many packages on pypi it wasn't a straightforward modification. Packaging in Python is an ongoing discussion and one of the reasons my ultimate goal is to publish a Debian package that can be installed and maintained via `apt-get`. It still had to be done.

{% hint style="info" %}
Take the time before starting a project and read a few _best practice guides_. This saves you a lot of time afterwards.
{% endhint %}

Since Taskbutler was my first Python project, the initial directory structure was a mess. [Cookiecutter](https://github.com/audreyr/cookiecutter-pypackage) is a project that helps to get it right in the first time. Cookiecutter creates complete project structures with the help of templates. But since their templates are maintained by _random people on the internet_ it's often not as easy as the _quickstart_ states. It's a start - but to use it in my already existing project I generated the cookie-cutter project in a different directory and only moved the files I understood into my project. Even then I run into issues with using Windows as an OS and with the template using an old version of _bumpverison_.

{% hint style="info" %}
Always check the issues at GitHub for known problems.
{% endhint %}

I run into an issue with _bumpversion_ that already has been documented in the issues. It saves time to check open(and even closed) issues; It also gives an idea about how the project is maintained. Using abandoned projects, examples or how-tos can cost a lot of time fixing and researching incompatibility issues.

 There is never a guide that meets all individual requirements. It's even worse for Python since some helpful projects or templates are specifically for a Python version or an operating system. Many
Unfortunately, many helpful projects are outdated and so, it's still important to remember the steps and develop a personal vision of _the perfect project_.

develop a personal idea of   _ But even then, different people have different opinions on _the perfect project_ and so, It helps to make mistakes. Every mistake from the first project is one less in the second. Since _so many_ helpful pip packages are outdated, it helps to develop a personal idea of _
