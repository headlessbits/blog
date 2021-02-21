---
title: "Birth of This Blog"
date: 2021-02-20T23:21:57+06:00
description: "How this blog site came to existence"
tags: ["misc"]
author: "Fazle Rabbi"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
searchHidden: true
cover:
    image: "" # image path/url
    alt: "" # alt text
    caption: "" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---
## Intro

A blog, a truncation of "web-log" is a diary of an entity, that logs the journey of the entity in the web. The entity can be a person, an organization, a company or an object. Nowadays almost everyone has a blog and in that they 'logs' their thoughts, opinions and discoveries. For a organization a blog is very helpful in sharing knowledge with the members and showcasing the works being done. As we started working on in Headless Bits, within a week felt the need to have a place where we can share our bits and pieces of knowledge among ourselves. Thus this blog is born.

The first blog about how this blog is deployed. This is more of a record rather then knowledge share but it just a baby step. Keep an eye on, more to come.

First the tech stack. This site usages the static site generator [Hugo](https://gohugo.io/), hosted in [GitHub](https://github.com/) and deployed using [GitHub Action](https://github.com/features/actions) and [GitHub Pages](https://pages.github.com/).

Hugo has a huge collections of themes for various purpose. After a some demo visiting and feature comparing, we decided to use [PaperMod](https://github.com/adityatelange/hugo-PaperMod) for our blog.

![PaperMod Screenshot](/image/birth-of-this-blog-screenshot-papermod.png)

PaperMod has all the functionalities we need without the extra fat. A nice looking landing page, dark mode (yei, 30% productivity boost!), post organization with category and tag, search. RSS, share article are few major functionalities. The full list of feature and functionalities can be seen in this [GitHub Wiki](https://github.com/adityatelange/hugo-PaperMod/wiki/Features)

## Setting up the blog with Hugo

So, let's get into the fun part of settings things up. All we need is a terminal access to work on `hugo` CLI tool, `git`, a text editor (preferably with markdown support) and a browser to access the webpages. I am using Ubuntu 20.04 with default GNOME Terminal, apt installed git, vim and Firefox but you can pick your own tools to suit your need. We will also need a [GitHub](https://github.com/) account.

We are using a custom domain for our blog site which is [`https://headlessbits.com/blog`](https://headlessbits.com/blog). For this demo we will use [`https://headlessbits.com/blog-demo`](https://headlessbits.com/blog-demo). This is optional and has some quarks of it's own. As we will see in Hugo's configuration.

First installing Hugo. If we follow the [Install Hugo](https://gohugo.io/getting-started/installing/) Doc on Hugo's site we can follow our specific OS instructions to install Hugo. For Ubuntu 20.04, it is as easy as doing `sudo apt install hugo`. Keep in mind that with `apt` we get a bit old version of Hugo from the Ubuntu repo, not the latest one. For latest one we can use the from the same doc page.

Now we need to open our favorite browser and go to [GitHub](https://github.com/) and sign in to our account. Then we will create a repo by clicking the `+` icon to the left of our profile avatar.

![create new repo](/image/birth-of-this-blog-create-new-repo.png)

The repo will have Public visibility. I am creating a new repo for this blog demo and naming it 'blog-demo'. Additionally, we can add a README.md and some description. I am not using any description for the demo. 

![give it a name, public visibility and add a README.md](/image/birth-of-this-blog-name-visibility.png)

Now we will clone the repo to our local workspace.

    git clone git@github.com:headlessbits/blog-demo.git

As we can see I am cloning with SSH and setting it up is out of scope of this article but I will leave the doc [link](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh) here.

With `hugo` installed and an empty git repo we are ready to start a Hugo site.

    hugo new site blog-demo/ --force

| `--force` is used because the repo is not empty as README.md exist.
| --- |

This would show the congratulatory message from Hugo.

	Congratulations! Your new Hugo site is created in /home/fazlerabbi37/fr37/temp/blog-demo.

	Just a few more steps and you're ready to go:

	1. Download a theme into the same-named folder.
	   Choose a theme from https://themes.gohugo.io/ or
	   create your own with the "hugo new theme <THEMENAME>" command.
	2. Perhaps you want to add some content. You can add single files
	   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
	3. Start the built-in live server via "hugo server".

	Visit https://gohugo.io/ for quickstart guide and full documentation.

This welcome message talks about how to add a theme, add content and start the built-in server. We will see all this steps one by one. We already have our theme selected. Let's install the theme following the themes [Install doc's Method 2](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation#method-2).

	cd blog-demo
	git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1
	git submodule update --init --recursive



Now we need to configure the site for PaperMod. For this we will heavily use the [PaperMod example site](https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite). Let's start by downloading `config.yml` that will replace the `config.toml` provided by Hugo.

	wget https://raw.githubusercontent.com/adityatelange/hugo-PaperMod/exampleSite/config.yml
	rm config.toml

Now we will modify the `config.yml` file to modify and remove things according to our need. I am going to describe what we did but it is very easy to understand. For us we changed the `baseURL`, `title` and `theme`. For us the `baseURL` is `https://headlessbits.com/blog-demo/` and the `theme` name would be `PaperMod` as this is what we used while cloning. We are not interested in the Google Analytics so I am deleting that line. In the `minify` section I am enabling `minifyOutput`. In language I am going to keep only English. Keeping the output as it is we move on to `params`. Here we changed the `description` and `author`. Set the `defaultTheme` to `dark` then jumped to `homeInfoParams` and changed `Title` and `Content`. For `socialIcons` only GitHub and RSS was kept. Now we save the `config.yml` file and start the Hugo's built-in server.

	hugo server -D

| `-D` is used for building the drafts.
| --- |

It show us the build statics showing something like this

	
					   | EN  
	-------------------+-----
	  Pages            | 11  
	  Paginator pages  |  0  
	  Non-page files   |  0  
	  Static files     |  0  
	  Processed images |  0  
	  Aliases          |  1  
	  Sitemaps         |  1  
	  Cleaned          |  0  

	Built in 35 ms
	Watching for changes in /path/to/blog-demo/{archetypes,content,data,layouts,static,themes}
	Watching for config changes in /path/blog-demo/config.yml
	Environment: "development"
	Serving pages from memory
	Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
	Web Server is available at http://localhost:1313/blog-demo/ (bind address 127.0.0.1)
	Press Ctrl+C to stop

| See the different at second last line. Our blog is published at `http://localhost:1313/blog-demo/` if you are not using a sub directory, it would simply be `http://localhost:1313/`
| --- |

Now let's open the URL in a browser and we should see the basic landing page.

![Headless Bits Blog landing page](/image/birth-of-this-blog-landing.png)

Now is a great time to commit and push our local changes to remote repo. We can do this with:

	# stop the server with Ctrl+C first, if it is still running
	git add *
	git commit # or git commit -m "added basic site"
	git push
	
Clicking around on 'Archive' and 'Search' we get 404 error! Nothing to worry. We are getting 404 error because we don't have those pages. Let's grab them from [PaperMod example site](https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite).

	wget -O content/archives.md https://raw.githubusercontent.com/adityatelange/hugo-PaperMod/exampleSite/content/archives.md
	wget -O content/search.md https://raw.githubusercontent.com/adityatelange/hugo-PaperMod/exampleSite/content/search.md

Let's add and push them to GitHub just like before:

	git add content/archives.md content/search.md
	git commit # or git commit -m "added archives.md and search.md"
	git push

If we start the server now the pages should be visible. With that done let's get on with creating a post. In Hugo we need a basic skeleton structure for a post which Hugo calls archetype and keeps them in the `archetypes` directory. We will crate `post.md` file in side archetypes directory and use the [Sample Page.md](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation#sample-pagemd) from PaperMod Installation Wiki to populate it and modify.

	vim archetypes/post.md

if you are also using vim, remember to set paste and paste all content from Sample Page.md. The title and date is fixed which I don't like. We will replace them with dynamic Hugo variables. The final result would look something like this.

	---
	title: "{{ replace .TranslationBaseName "-" " " | title }}"
	date: {{ .Date }}
	description: ""
	tags: [""]
	author: ""
	showToc: true
	TocOpen: false
	draft: true
	hidemeta: false
	comments: false
	disableHLJS: true # to disable highlightjs
	disableShare: false
	disableHLJS: false
	searchHidden: true
	cover:
		image: "" # image path/url
		alt: "" # alt text
		caption: "" # display caption under cover
		relative: false # when using page bundles set this to true
		hidden: true # only hide on current single page
	---

Update the GitHub repo again:

	git add archetypes/post.md
	git commit # or git commit -m "added post.md archetype"
	git push

Now let's create a test post.

	hugo new post/test.md

It would show:

	/path/to/blog-demo/content/post/test.md created

let's open `content/post/test.md` and edit the markdown file to add some content. After saving the file with some content we see that the title and date is auto populated so it seems to work!

	---
	title: "Test"
	date: 2021-02-20T19:20:44+06:00
	description: "test"
	tags: ["test"]
	author: "test"
	showToc: true
	TocOpen: false
	draft: true
	hidemeta: false
	comments: false
	disableHLJS: true # to disable highlightjs
	disableShare: false
	disableHLJS: false
	searchHidden: true
	cover:
		image: "" # image path/url
		alt: "" # alt text
		caption: "" # display caption under cover
		relative: false # when using page bundles set this to true
		hidden: true # only hide on current single page
	---

	This is a test post!

Navigating to our site at [`http://localhost:1313/blog-demo/`](http://localhost:1313/blog-demo/) we see that we have our new test post. It also show that it is a draft post.

![new post](/image/birth-of-this-blog-new-post.png)

If we click on the Test post we see the post page with our title, description, data, reading length, author and table of content. We also see the content and tag bellow. The share to social feature is working as well.

![post page](/image/birth-of-this-blog-post-page.png)

We will push this test post to GitHub but before we do that we need to edit test.md and change the metadata draft to false from true. Now we push to GitHub:

	git add content/post/test.md
	git commit # or git commit -m "added test.md new post"
	git push

## Deploy

We will use [GitHub Action](https://github.com/features/actions) to deploy our site. For Hugo we have many opinions to choose from. The most stared and dead simple one is [Hugo setup](https://github.com/marketplace/actions/hugo-setup#%EF%B8%8F-create-your-workflow). Before we set up the action workflow we need to create a Personal access token and add it to our repo as secret which will allow GitHub Actions to push to our repo and deploy the site.

To generate Personal access token go to Settings from user avatar.

![settings from user avatar](/image/birth-of-this-blog-settings-from-user-avatar.png)

Then Developer settings at the bottom of the left side menu.

![developer settings](/image/birth-of-this-blog-developer-settings.png)

Then click on Personal access token on the left side menu.

![personal access token](/image/birth-of-this-blog-personal-access-token.png)

Now click on Generate new token.

![generate new token](/image/birth-of-this-blog-generate-new-token.png)

On the token generation page give the token a Note. I am using `headless-bits-blog-demo-hugo` as note. Then click on the `repo` checkbox and it would check all the box under `repo`.
 
![token generation page](/image/birth-of-this-blog-token-generation-page.png)

Now scroll down and click Generate token button. In the next page you should get a 40 character long alpha numeric value which is your token. Copy it and keep it somewhere and don't share with anyone.

![generate token button](/image/birth-of-this-blog-generate-token-button.png)

Let's use the token to configure a secret in out blog-demo GitHub repo. For that we need to go to the Settings tab of the repo.

![repo settings](/image/birth-of-this-blog-repo-settings.png)

Scroll down a bit and click on Secrets on the left side menu.

![secrets sub menu](/image/birth-of-this-blog-secrets-sub-menu.png)

Click on New repository secret.

![new repository secret](/image/birth-of-this-blog-new-repository-secret.png)

Give it a name like `DEMO_SECRET` and paste the 40 character long alpha numeric personal access token. Then click Add secret.

![add secret](/image/birth-of-this-blog-add-secret.png)

Now finally we will add the GitHub action workflow.

To add GitHub action workflow, click on the Actions tab on the top ribbon of the menu. 

![actions tab](/image/birth-of-this-blog-actions-tab.png)

Click on `set up a workflow yourself`. 

![set up a workflow yourself](/image/birth-of-this-blog-set-up-a-workflow-yourself.png)

It will open the online file editor to edit `main.yml` inside `.github/workflows` directory. We can choose to change the file name if needed but I am keeping it as it is. Now we need to Hugo setup actions Getting started -> [Create your workflow](https://github.com/marketplace/actions/hugo-setup#%EF%B8%8F-create-your-workflow) part. Copy the yaml code from `name` to `./public` in it's entirety and paste it in the `main.yml` file. Make sure to change the `branches` to match your main branch and `github_token` to the name given in the 'Add secret' step. For us the `main.yml` file look likes this:

	name: github pages

	on:
	  push:
		branches:
		  - master  # Set a branch to deploy

	jobs:
	  deploy:
		runs-on: ubuntu-18.04
		steps:
		  - uses: actions/checkout@v2
			with:
			  submodules: true  # Fetch Hugo themes (true OR recursive)
			  fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

		  - name: Setup Hugo
			uses: peaceiris/actions-hugo@v2
			with:
			  hugo-version: '0.79.1'
			  # extended: true

		  - name: Build
			run: hugo --minify

		  - name: Deploy
			uses: peaceiris/actions-gh-pages@v3
			with:
			  github_token: ${{ secrets.DEMO_SECRET }}
			  publish_dir: ./public

Now click on Start commit button.

![start commit](/image/birth-of-this-blog-start-commit.png)

Write a nice commit message like 'create main.yml to publish site with hugo' and click on Commit new file. 

![commit new file](/image/birth-of-this-blog-commit-new-file.png)

Now click on Code tab.

![code tab](/image/birth-of-this-blog-code-tab.png)

We will see a yellow dot on the left of your commit which means the actions is running.

![the commit with yellow dot](/image/birth-of-this-blog-the-commit-with-yellow-dot.png)

If we click on the yellow dot we see a bit more details and clicking on details takes us to more details page for the action.

![action details](/image/birth-of-this-blog-action-details.png)

Upon successful completion we see a green check mark on the left side of our commit.

![the green mark of success](/)

Now we need to setup the GitHub Pages. Click on the Settings Tab of the repo.

![settings tab of the repo](/image/birth-of-this-blog-settings-tab-of-the-repo.png)

Scroll down to GitHub Pages section. For us the site is published at [`http://headlessbits.com/blog-demo/`](http://headlessbits.com/blog-demo/) because we have a site published at [`http://headlessbits.com/`](http://headlessbits.com/blog-demo/) with GitHub Pages and after the first one all repos by default usages the $DOMAIN.TLD/$REPO_NAME format. See this [doc](https://docs.github.com/articles/using-a-custom-domain-with-github-pages/) to know more.

![GitHub Pages domain name](/image/birth-of-this-blog-github-pages-domain-name.png)

Make sure that branch is set to `gh-pages` and folder is `/ (root)`. Click on Enforce HTTPS check box as well.

![GitHub Pages branch and HTTPS](/image/birth-of-this-blog-github-pages-branch-and-https.png)

Now let's check the site live at [`http://headlessbits.com/blog-demo/`](http://headlessbits.com/blog-demo/).

![yee haw the live site!](/image/birth-of-this-blog-yee-haw-the-live-site.png)

We see our test post is live. Clicking on the box takes us to the post page

![post page in live site](/image/birth-of-this-blog-post-page-in-live-site.png)

Yeaa! We have successfully deployed our site using Hugo, GitHub Action and GitHub pages!

We made one more minor change in our original site that changed the footer to add our main sites link. It is as easy as coping the `footer.html` from themes directory to layout directory in root

	mkdir -p layouts/partials/
	cp themes/PaperMod/layouts/partials/footer.html layouts/partials/

and modify the file to add one line of HTML

	<span>&copy; {{ now.Year }} <a href="https://headlessbits.com">Headless Bits</a></span>

Hope this helped you to deploy your blog or at least helped you in someways to get your presence online. Cheers!
