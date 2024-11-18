---
related:
  - "[[Quartz]]"
completed: true
Main Moc: "[[Tech MOC]]"
created: 2024-03-19
updated: 2024-10-17T22:27
---
This website is built using [Quartz](https://quartz.jzhao.xyz/), a tool that transforms your Markdown notes into a static website. 

On this page, I've outlined every step I took to make the site look and behave as you see it.

Most of the setup follows the official [Quartz documentation](https://quartz.jzhao.xyz/#-get-started), but I've also done some modification mainly on the colours and page layouts.

One thing I did differently was use [[Git Submodules]] to store my content. This means that my website's content ([my obsidian vault](https://github.com/rimaout/Obsidian-Vault)) is kept in a separate repository.

## Steps

>[!note] Clone Repository
>```shell
>git clone https://github.com/jackyzha0/quartz.git
>cd quartz
>npm i
>npx quartz create
>```

>[!note] Add Git Submodule
>Add [[Git Submodules|Git Submodule]] as content:
>1. Go in Quartz directory
>2. Run: 
>	```shell
>	git submodule add https://github.com/username/repo.git content/vault
>	git commit -m "Added a new submodule for obsidian notes"
>	```
>	
>>[!warning]- How to update the content
>>1. Go in Obsidian vault, commit and push all changers
>>2. Go to Quartz directory
>>3. Run: `git submodule update --remote content/vault` to update content directory\
>>4. Run `npx quartz sync` to push the changes

>[!note] Add Index File
>1. Go in `quartz/content/Index.md`
>2. Write this: [[Quartz Index Example]]

>[!note] Add `deploy.yaml` to deploy on Github
>1. Go in to quartz directory
>2. Create and write `deploy.yaml` in `quartz/.github/workflows/deploy.yml`:
	>```shell
	>nvim quartz/.github/workflows/deploy.yml  
	>```
>3. Write this in the file: [[Quartz deploy.yaml]]

>[!note] Edit Config File
>1. Go to quartz root directory 
>2. Edit `quartz.config.ts`: 
>	- `pageTitle: "Notes in Public",`
>	- `analytics: null,`
>	- `baseUrl: "notesinpublic.xyz",`
>3. Edit colours: [[My Quartz Theme]]

>[!note] Edit Layout
>1. Go to quartz root directory 
>2. Edit `quartz.config.ts`
>3. Write this in the file: [[quartz layout config]]

>[!note] Edit Page Width
>1. Go to quartz root directory
>2. Go to `quartz/styles`
>3. Edit `variable.css`, in particular set:
>	- `mobile: 900px`
>	- `desktop: 1380px`

>[!note] Add Custom Icon and Banner
>1. Go to quartz root directory 
>2. Go to `quartz/static`
>3. Substitute the `icon.png` image in the directory with this: [[icon.png]]
>4. Substitute the `og-image.png` image in the directory with this: [[og-image.png]]

>[!note] Add Icon Credits
>1. Go to quartz root directory
>2. Go to `quartz/componets`
>3. Edit `footer.tsx` like this: [[Quartz Footer Edit]]

>[!note] Edit README
>1. Go to quartz root directory
>2. Edit the `README.md` line this: [[New Quartz README]]
>   
>**Also:** Also remove code of conduct and license files

>[!note] Upload to GitHub
>1. Make a blank git repository (no readme, no license, no code of conduct)
>2. Then, run the following commands, replacing `REMOTE-URL` with the URL of your new repository.
>	
>	```shell
>	# list all the repositories that are tracked
>	git remote -v
>	```
>	
>	 ```shell
>	# if the origin doesn't match your own repository, set your repository as the origin
>	git remote set-url origin REMOTE-URL
>	 ```
>	
>	```shell
>	# if you don't have upstream as a remote, add it so updates work
>	git remote add upstream https://github.com/jackyzha0/quartz.git
>	```
>
>3. run `npx quartz sync --no-pull` to upload to Github

>[!note] Set Github Pages
>1. Go to GitHub
>2. Open the repository used to host [[Quartz]]
>3. Go to settings
>4. Go to Pages section 
>5. Select `git up actions` in Source
>6. Set custom domain if you have one (see how [here](https://quartz.jzhao.xyz/hosting#custom-domain))
>7. Go to Environment section and delete all the environments



