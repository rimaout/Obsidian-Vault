---
related:
  - "[[Quartz]]"
completed: true
Main Moc: "[[Tech MOC]]"
created: 2024-03-19
updated: 2025-09-23T19:32
---
This website is built using [Quartz](https://quartz.jzhao.xyz/), a tool that transforms your Markdown notes into a static website. On this page, I've outlined every step I took to make the site look and behave as you see it.

Most of the setup follows the official [Quartz documentation](https://quartz.jzhao.xyz/#-get-started), but I've also done some modification mainly on the colors and page layouts. One thing I did differently was use [[Git Submodules]] to store my content. This means that my website's content ([my obsidian vault](https://github.com/rimaout/Obsidian-Vault)) is kept in a separate repository.

## Steps

>[!note] Clone Repository
>```shell
>git clone https://github.com/jackyzha0/quartz.git
>cd quartz
>npm i
>npx quartz create
>```

>[!note] Add Git Submodule
>
>
>Add [[Git Submodules|Git Submodule]] as content:
>1. Go in Quartz directory
>2. Run: 
>	```shell
>	git submodule add https://github.com/username/repo.git content/vault
>	git commit -m "Added a new submodule for obsidian notes"
>	```
>	
>>[!warning] How to update the content
>>
>>**Simple Method:**
>>In this method we have to manually update the submodule in the content directory:
>>1. Go in Obsidian vault, commit and push all changers
>>2. Go to Quartz directory
>>3. Run: `git submodule update --remote content/vault` to update submodule in content directory
>>4. Run `npx quartz sync` to push the changes
>>   
>>**Advanced Method:**
>>In this method we use a workflow to automagicaly update the submodule each time the repo of the submodule is modified.
>>- ***Read:*** [[Using GitHub Actions to automatically update repo's submodules]]

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
>	- `sidePanelWidth: 300px;`

>[!note] Add Custom Icon and Banner
>1. Go to quartz root directory 
>2. Go to `quartz/static`
>3. Substitute the `icon.png` image in the directory with this: [[icon.png]]
>4. Substitute the `og-image.png` image in the directory with this: [[og-image.png]]

>[!note] Add custom CSS
>I have made some modifications on how the Bold and italic text behave and made the images center align.
>
>Click [[Quartz custom CSS|here]] to se what I have changed.

>[!note] Add Icon Credits
>1. Go to quartz root directory
>2. Go to `quartz/componets`
>3. Edit `footer.tsx` like this: [[Quartz Footer Edit]]

>[!note] Add Grid Layout for Callouts
>
>Here is how to make it: [[Quartz Callouts Grid Layout]].
>
>![[callouts_grid_layout.webp|900]]


>[!note] Add icon to site Title
>Here is [[How to add custom icon to site title - Quartz|how to make it]].
>
>![[Screenshot 2024-12-04 at 08.10.26.png|600]]

>[!note] Edit README
>1. Go to quartz root directory
>2. Edit the `README.md` like this: [[New Quartz README]]
>   
>**Also:** Also remove code of conduct and license files

>[!note] Upload to GitHub
>3. Make a blank git repository (no readme, no license, no code of conduct)
>4. Then, run the following commands, replacing `REMOTE-URL` with the URL of your new repository.
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
>5. run `npx quartz sync --no-pull` to upload to Github

>[!note] Set Github Pages
>6. Go to GitHub
>7. Open the repository used to host [[Quartz]]
>8. Go to settings
>9. Go to Pages section 
>10. Select `git up actions` in Source
>11. Set custom domain if you have one (see how [here](https://quartz.jzhao.xyz/hosting#custom-domain))
>12. Go to Environment section and delete all the environments



