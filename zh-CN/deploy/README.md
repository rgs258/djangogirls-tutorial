# 部署！

> **注意** 以下章节有时可能难以完成。 坚持并完成它 ；部署是在网站开发过程的重要组成部分。 这一章放在本教程的中部，因此你的指导者可以帮助你在使网站上线中的一些小困难。 这意味着如果您花大量的时间，你仍然能独立完成这个教程。

直到现在，您的网站只能在您的计算机上访问， 现在你要会学习如何部署它！ 部署是在互联网上发布你的应用程序的一系列过程，因此人们最终可以一起去看看你的应用程序. :)

正如你所学习的，一个网站必须要放到一个服务器上。 互联网上有许多服务器供应商，我们将使用 [PythonAnywhere](https://www.pythonanywhere.com/)。 PythonAnywhere 对于一些没有太多访问者的小应用是免费的，所以它对你来说绝对是足够使用的。

其它我们将使用到的外部服务是[GitHub](https://www.github.com)，它是一个代码托管服务。 还有其它的一些服务，但当今几乎所有的程序员都有 GitHub 帐户，并且现在你也会有的！

这三个地方对于你来说很重要。 您的本地计算机将是您开发和测试的地方。 当您高兴地看到更改时，您将在GitHub上放置您的程序副本。 您的网站在PythonAnywhere上部署并通过从GitHub上获取新的代码副本来更新。

# Git

> **注意** 如果你已经做过安装步骤了，你可以直接跳过这个步骤开始创建你自己的Git版本库。

{% include "/deploy/install_git.md" %}

## 开始我们自己的Git版本库

Git跟踪一组特定的在代码仓库（或简称“仓库”）中文件的更改。 我们开始用git管理自己的项目吧。 打开你的终端，进入 `djangogirls` 文件夹运行以下的命令：

> **注意** 在初始化仓库之前，请使用 `pwd`命令 (OSX/Linux) 或者 `cd` (Windows) 命令检查你当前的工作目录。 你应该是在 `djangogirls` 文件夹下运行命令。

{% filename %}command-line{% endfilename %}

    $ git init
    Initialized empty Git repository in ~/djangogirls/.git/
    $ git config --global user.name "Your Name"
    $ git config --global user.email you@example.com
    

每个项目我们只需要初始化一次Git仓库（而且你从此不需要重新输入用户名和邮箱）。

Git会追踪这个目录下所有文件和文件夹的更改，但是有一些文件我们希望Git忽略它。 为此，我们可以在系统根目录下创建一个命名为 `.gitignore` 的文件。 打开编辑器，创建新文件并写入以下内容：

{% filename %}.gitignore{% endfilename %}

    *.pyc
    *~
    /.vscode
    __pycache__
    myvenv
    db.sqlite3
    /static
    .DS_Store
    

然后在djangogirls项目根目录下将它保存为 `.gitignore`文件。

> **注意** 在文件名最前面的"."很重要。 如果你在创建文件的时候有困难(例如，Macs不能通过Finder创建开头为"."的文件), 可以在编辑器里点击"另存为", 这个没问题的。 确定不添加<0 txt</code>,`><py`,或者文件名中的任何其他扩展名，只有在名称为 `gigistnow`的情况下，该扩展才能被Git 确认。
> 
> **注意** 您在 `githnode`文件中指定的文件之一是 `db.sqlite3`。 此文件是你的本地数据库，用来存储所有用户和帖子。 我们将遵循标准的网络编程做法，这意味着我们将使用单独的数据库来用于本地测试网站和您的 PythonAnywhere 上的现场网站。 PythonAnywhere 数据库可以像您的开发机器一样使用SQLite，但通常使用一个叫MySQL的站点访问者比SQLite更多。 无论如何，无视您GitHub 复制的SQLite数据库意味着您迄今所创建的所有帖子和超级用户只能在当地使用，并且您必须在生产中创建新的版本。 你应该把本地数据库视为一个可以随意测试不同的事情而不担心你会从博客中删除您的真实帖子的地方。

在执行git操作之前，最好使用 `git status` 命令查看一下当前的状态，尤其是在执行 `git add`或者在你不确定哪些文件被改动的情况下。 这有助于阻止各种意外发生，例如错误的文件被添加或提交。 `git status` 命令会返回所有未追踪/修改/暂存的文件，还有分支状态等信息。 输出将类似于以下内容：

{% filename %}command-line{% endfilename %}

    $ git status
    On branch master
    
    No commits yet
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
            .gitignore
            blog/
            manage.py
            mysite/
            requirements.txt
    
    nothing added to commit but untracked files present (use "git add" to track)
    

最后保存我们的更改。转到你的控制台并运行这些命令：

{% filename %}command-line{% endfilename %}

    $ git add --all .
    $ git commit -m "My Django Girls app, first commit"
     [...]
     13 files changed, 200 insertions(+)
     create mode 100644 .gitignore
     [...]
     create mode 100644 mysite/wsgi.py
    

## 将您的代码推送至 GitHub

转到 [GitHub.com](https://www.github.com) 并注册一个新的免费用户帐户。 (如果您已经做完了这步，那很棒) 请确认记住了您的密码(如果您使用密码，添加到您的密码管理器)。

现在，创建一个新的仓库，命名为“my-first-blog”。 保持 "initialise with a README" 选框未选中状态，.gitignore 选项为无 (我们已经手动创建了) ，让License设置为无。

![](images/new_github_repo.png)

> **注意** `my-first-blog`这个名字很重要，你可以用其它的，但是这个名字会在教程中出现多次，你需要确保每次都替换掉它。 保持用 `my-first-blog` 这个名字可能更为简单.

在下一个屏幕上，您将显示你的仓库克隆URL，您将会在下面的一些命令中使用：

![](images/github_get_repo_url_screenshot.png)

现在我们需要把你计算机上的Git仓库绑定到 GitHub 上。

Type the following into your console (replace `<your-github-username>` with the username you entered when you created your GitHub account, but without the angle-brackets -- the URL should match the clone URL you just saw):

{% filename %}command-line{% endfilename %}

    $ git remote add origin https://github.com/<your-github-username>/my-first-blog.git
    $ git push -u origin master
    

When you push to GitHub, you'll be asked for your GitHub username and password (either right there in the command-line window or in a pop-up window), and after entering credentials you should see something like this:

{% filename %}command-line{% endfilename %}

    计数对象：6, 完成。
    Writing objects: 100% (6/6), 200 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To https://github.com/ola/my-first-blog.git
    
     * [new branch]      master -> master
    Branch master set up to track remote branch master from origin.
    

<!--TODO: maybe do ssh keys installs in install party, and point ppl who dont have it to an extension -->

现在你的代码已经在GitHub上了。 快去确认一下吧！ 你会发现这是一个很好的平台-[Django](https://github.com/django/django), the [Django Girls Tutorial](https://github.com/DjangoGirls/tutorial)，还有很多其他非常棒的开源软件项目也将他们的代码放在GitHub上。 :)

# 在 PythonAnywhere 设置我们的博客

## 注册一个 PythonAnywher 帐户

> **Note**您可能已经在安装步骤的早期创建了 pythonanywhere 帐户-如果是的话, 则无需重复。

{% include "/deploy/signup_pythonanywhere.md" %}

## 在 pythonanywhere 配置我们的网站

点击图标回到 [PythonAnywhere 主控制面板](https://www.pythonanywhere.com/) ，然后选着启动 "Bash" 控制台的选项-即PythonAnywhere版本的命令行，就像你的计算机的命令行一样。

![在 PythonAnywher 网页界面上 '新建控制台' 部分，按钮为 'bash'](images/pythonanywhere_bash_console.png)

> **注意** PythonAnywhere 基于 Linux系统，因此如果你使用 Windows系统，控制台将会和你本地电脑上的略有不同。

在 pythonanywhere 上部署 web 应用程序涉及从 github 中提取代码, 然后配置 pythonanywhere 以识别它并开始将其作为 web 应用程序提供。 有许多手工操作方式，但是 PythonAnywhere已经提供了帮助工具为你代劳。 让我们先安装它：

{% filename %}PythonAnywhere 命令行{% endfilename %}

    $ pip3.6 install --user pythonanywhere
    

这应该列印出一些内容，例如 `收集 pythonanywhere`，并最终以 `Successfully installed (...) pythonanywhere- (...)`结束.

现在我们运行帮助来自动配置我们在GitHub的应用程序。 在 PythonAnywhere 控制台输入以下(不要忘记用你在GitHub用户名来代替 `<your-github-username>`, 以便URL 与GitHub克隆的URL匹配）：

{% filename %}PythonAnywhere 命令行{% endfilename %}

    $ pa_autoconfigure_django.py --python=3.6 https://github.com/<your-github-username>/my-first-blog.git
    

当你看到其运行时，你会看到它所做的事情：

- 从GitHub下载你的代码
- 在 PythonAnywhere上创建一个virtualenv，就像你自己在你的电脑上的那个一样
- 使用一些部署设置来更新您的设置文件。
- 使用 `manage.py migrate` 命令来在 PythonAnywhere创建一个数据库
- 是指你的静态文件（我们稍后会了解这些文件）
- 配置PythonAnywhere，并通过其API来为你的网页程序提供服务

在 PythonAnywhere上，所有的这些步骤都会自动的，但是他们和你在其他服务器提供的步骤是一样的。

The main thing to notice right now is that your database on PythonAnywhere is actually totally separate from your database on your own computer, so it can have different posts and admin accounts. As a result, just as we did on your own computer, we need to initialize the admin account with `createsuperuser`. PythonAnywhere has automatically activated your virtualenv for you, so all you need to do is run:

{% filename %}PythonAnywhere command-line{% endfilename %}

    (ola.pythonanywhere.com) $ python manage.py createsuperuser
    

Type in the details for your admin user. Best to use the same ones as you're using on your own computer to avoid any confusion, unless you want to make the password on PythonAnywhere more secure.

Now, if you like, you can also take a look at your code on PythonAnywhere using `ls`:

{% filename %}PythonAnywhere command-line{% endfilename %}

    (ola.pythonanywhere.com) $ ls
    blog  db.sqlite3  manage.py  mysite requirements.txt static
    (ola.pythonanywhere.com) $ ls blog/
    __init__.py  __pycache__  admin.py  apps.py  migrations  models.py
    tests.py  views.py
    

You can also go to the "Files" page and navigate around using PythonAnywhere's built-in file browser. (From the Console page, you can get to other PythonAnywhere pages from the menu button in the upper right corner. Once you're on one of the pages, there are links to the other ones near the top.)

## You are now live!

Your site should now be live on the public Internet! Click through to the PythonAnywhere "Web" page to get a link to it. You can share this with anyone you want :)

> **Note** This is a beginners' tutorial, and in deploying this site we've taken a few shortcuts which aren't ideal from a security point of view. If and when you decide to build on this project, or start a new project, you should review the [Django deployment checklist](https://docs.djangoproject.com/en/2.2/howto/deployment/checklist/) for some tips on securing your site.

## Debugging tips

If you see an error while running the `pa_autoconfigure_django.py` script, here are a few common causes:

- Forgetting to create your PythonAnywhere API token.
- Making a mistake in your GitHub URL
- If you see an error saying *"Could not find your settings.py"*, it's probably because you didn't manage to add all your files to Git, and/or you didn't push them up to GitHub successfully. Have another look at the Git section above
- If you previously signed up for a PythonAnywhere account and had an error with collectstatic, you probably have an older version of SQLite (eg 3.8.2) for your account. In that case, sign up for a new account and try the commands in the PythonAnywhere section above.

If you see an error when you try to visit your site, the first place to look for some debugging info is in your **error log**. You'll find a link to this on the PythonAnywhere ["Web" page](https://www.pythonanywhere.com/web_app_setup/). See if there are any error messages in there; the most recent ones are at the bottom.

There are also some [general debugging tips on the PythonAnywhere help site](http://help.pythonanywhere.com/pages/DebuggingImportError).

And remember, your coach is here to help!

# 查看你的网站！

The default page for your site should say "It worked!", just like it does on your local computer. Try adding `/admin/` to the end of the URL, and you'll be taken to the admin site. Log in with the username and password, and you'll see you can add new Posts on the server -- remember, the posts from your local test database were not sent to your live blog.

Once you have a few posts created, you can go back to your local setup (not PythonAnywhere). From here you should work on your local setup to make changes. This is a common workflow in web development – make changes locally, push those changes to GitHub, and pull your changes down to your live Web server. This allows you to work and experiment without breaking your live Web site. Pretty cool, huh?

Give yourself a *HUGE* pat on the back! Server deployments are one of the trickiest parts of web development and it often takes people several days before they get them working. But you've got your site live, on the real Internet!