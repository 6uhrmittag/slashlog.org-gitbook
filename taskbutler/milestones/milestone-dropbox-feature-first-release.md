[Milestone: Dropbox Feature - First release](https://github.com/6uhrmittag/taskbutler/milestone/1)

# [Rebranding](https://github.com/6uhrmittag/taskbutler/issues/14)

As discussed in [naming your tool](../../bashblog/naming.html), naming a tool is a great way to ensure it's quality. But naming a tool has also practical implications. When using APIs it's often required to register the app with its name. Since with this milestone I was using the Dropbox API, I had to find a pretty name for what was _todoist-progress_.

> You can't name your baby X

At this point, I already knew that Taskbutler will be a somewhat serious project and so I noticed an important part in the [Todoist API documentation](https://developer.todoist.com/sync/v7/#brand-usage):

> In addition, please take note of the following:
>
> * “Todoist” cannot be the first word in your application’s name. It can be used in the name of your app, though. For instance “x for Todoist” or “x with Todoist”, etc. This makes it clear that your application is created by you and not by Doist.
> * You must clearly state that your application is "not created by, affiliated with, or supported by Doist” in your application description.

This is quite understandable, but since this was my first time touching this topic, I took this quite seriously. After checking GitHub and google for similarly named projects, I went ahead and registered taskbutler.org. The rebranding itself was quite easy and I'm still proud if finding such a lovely name for this project.

# [Create dropbox paper and link to task](https://github.com/6uhrmittag/taskbutler/issues/20)

After successfully releasing the progress bar-feature, I dug a bit deeper into the universe of 3rd party APIs. Taskbutler motivated me to add more functionalities to the now multi-purpose task butler. Finding [Dropbox Paper](https://www.dropbox.com/en/paper) was pure luck. After using and disliking [Quip](https://quip.com/), I had high hopes for Dropbox Paper. I actually used it do brainstorm the Dropbox Paper functionality since it always bugged my how limited the Todoist comment-functionality is.  
A few years ago I tried [Atlassian's Confluence](https://confluence.atlassian.com/) + Jira for personal task tracking and knowledge management. It turned out pretty well, but it's just a tiny bit too expensive and produces a lot of overhead. It's also lacking a usable todo mobile app. Anyway...  
Dropbox Paper turned out to be a great tool to enhance normal tasks. After finding the official [Python SDK for Dropbox API v2](https://github.com/dropbox/dropbox-sdk-python) it was pretty easy to implement the basic functionality of creating and linking papers. Unfortunately the paper-API is still in development and I had to work around some limitations such as searching for papers.

The flow is pretty straightforward: 

1. The user creates a folder and an initial paper
2. Taskbutler searches for a task with a specific label name
3. checks if the task-title already contains an URL
4. If no URL is found:
   1. it creates a new Dropbox Paper with the task-title as content
   2. adds the URL to the Todoist task-title using Todoist's formatting syntax

The main issue is keeping the link between task and paper alive. Since no additional metadata can be stored within the task, Taskbutler relies on the URL in the task-title to be right.  
Additionally, I stumbled on two weird issues:

* the API can't find an empty folder - the user has to place an initial paper inside the folder
* the default permissions are set to public, which requires Taskbutler to always modify the permissions on new papers

# [Upload template to Dropbox and link task to Office365](https://github.com/6uhrmittag/taskbutler/issues/19)

This feature is pretty wild! It makes use of the Microsoft Office 365 integration in Dropbox.  
Once Office 365 is connected to Dropbox, it is possible to open Office documents directly from the web-view of Dropbox. The file will then open right inside office.com\(a web version of Word, Excel, Powerpoint\). 

The implementation is wild but super simple. It makes use of Dropbox URLs to Office 365 always following the same schema: [https://www.dropbox.com/ow/msft/edit/home/](https://www.dropbox.com/ow/msft/edit/home/)&lt;$FOLDER&gt;/&lt;$FILENAME&gt;

Once one is logged into Dropbox and clicks on a link like this, the corresponding file will open the web version of Microsoft Office. Since Todoist task-texts are clickable as soon as they contain a link, the integration is almost seamless. To make use of this feature Taskbutler will also upload a specified file template to Dropbox when the feature label is found.

My main goal is to make it super easy to write a simple letter in case of e.g. cancelling a contract or similar things that require a default template. It saves a ton of time to select and edit a template once and using it with this feature.

This feature opens up a whole world of similar workflows. I imagine e-mail templates or even integration of online fax-services that sends the finished letter once it's marked as done.

# [Test in production](https://github.com/6uhrmittag/taskbutler/issues/27)

At this point in development, I already noticed that the lack of tests is very problematic. I already added a devmode that works as a dry-run.   
But I still had to rely on real-life tests with my personal account and during my personal usage. The functionality was still very limited and so were the test cases, but I clearly noticed the issue of missing tests.

Even today the test coverage is not very high. That's why Taskbutler still fails very early and hard in case of any malfunction. Since Taskbutler modifies important user-data, it hopefully rather crashes completely than corrupts any Todoist data.

# [Log rotation](https://github.com/6uhrmittag/taskbutler/issues/25)

Unfortunately, this is one of those issues, that are easily avoidable with proper testing. After a few days of personal usage, I noticed logfiles a size 50-100MB. This was due to a debug-log that generated tons of data.

