---
Created: 2024-03-19
Related: []
Completed: 
Main Moc: "[[Tech MOC]]"
---
---
Clone repository:
```shell
git clone https://github.com/jackyzha0/quartz.git
cd quartz
npm i
npx quartz create
```

Add [[Git Submodules|Git Submodule]] as content:
1. go in quartz directory
2. Run: 
	```shell
	git submodule add https://github.com/username/repo.git content/vault
	git commit -m "Added a new submodule"
	```

Add Index file:
1. Go in `quartz/content/Index.md` and write this: [[Index]]

Add `deploy.yaml` to deploy on Github
1. Go to quartz directory
2. Create and write `deploy.yaml` in `quartz/.github/workflows/deploy.yml`:
	```shell
	nvim quartz/.github/workflows/deploy.yml  
	```
3. Write this in the file: [[quartz add deploy.yaml]]

Edit config file:
1. Go to quartz root directory 
2. Edit `quartz.config.ts`: 
	- `pageTitle: "Notes in Public",`
	- `analytics: null,`
	- `baseUrl: "notesinpublic.xyz",`
3. Edit colours: [[quartz theme]]

Edit layout file:
1. Go to quartz root directory 
2. Edit `quartz.config.ts`
3. Write this in the file: [[quartz layout config]]

Add Custom icon and banner and Title:

Upload to GitHub:
1. Make a blank git repository (no readme, no license, no code of conduct)
2. Then, run the following commands, replacing `REMOTE-URL` with the URL you just copied from the previous step.
	
	```shell
	# list all the repositories that are tracked
	git remote -v
	```
	
	 ```shell
	# if the origin doesn't match your own repository, set your repository as the origin
	git remote set-url origin REMOTE-URL
	 ```
	
	```shell
	# if you don't have upstream as a remote, add it so updates work
	git remote add upstream https://github.com/jackyzha0/quartz.git
	```

3. run `npx quartz sync --no-pull` to upload to Github

### Git hub pages
- Go to Github
- Open quartz repository
- Go to Quartz settings 
	- Go to Pages section and select `git up actions` in Source
	- Set custom domain: https://quartz.jzhao.xyz/hosting#custom-domain
	- Go to Environment section and delete all the environments

### Update README
- Remove license and code of conduct
- Update readme 



