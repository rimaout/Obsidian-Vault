---
created: 2025-01-01T21:51
updated: 2025-01-10T20:06
tags:
  - monthly-log
---
-- 🚧 work in progress, come back later 🚧 --

## 👻 Ghosty

The best Christmas gift i received this year was [Ghosty](https://github.com/ghostty-org)

## 🌐 Site Update

The pages of this site are just [markdown]() files that I write using [obsidian](https://obsidian.md/), than I use a tool called [quartz](https://quartz.jzhao.xyz/) to convert my obsidian vault in this website. 

There are different ways to make a site using quartz depending on the platform you want to use to host your site but the simplest and cheapest (it' free) way is to use GitHub, so that's what I did. The easiest and fastest way to set up quartz using Github it's just to clone the quartz official repo and than paste your obsidian vault inside the content directory. This is really easy to set up but it means that each time you want to update you content you have to manually copy and paste you vault in the content directory.

But I like automating things so I decided to use two separate repos one for quartz and one for the obsidian vault and than I created a submodule inside the content directory that links to the vault repo. This meant that I didn’t have to manually copy and paste the vault but I just had to run a command onside the quartz repo that updates the submodule.

```bash
git submodule update --remote content/vault
```

This is how I have always updated my site content, but there is not fully autonomous because I still had to open the terminal write write the commands and push the changes. So this month I spend some time learning about git submodules, Github secrets and actions and I have been able to use this things to completely automate the site content update. Now each time I push the changes of my obsidian vault to Github the quartz repo is notified about the change and *automagicaly* updates all the submodules. 

If you want to learn how to do this, I have written a [[Using GitHub Actions to automatically update repo's submodules|small guide]], and if you want to replicate my site here is how i have made it [[Quartz Setup]].

**What I'm reading:**

**Video of the Month:**

## Other

- **TODO:** The world of lana, screenshots
- top study playlist: https://open.spotify.com/album/0CZbWkuYjXiZlmSsQz48oi

---

>**See all the other monthly logs:** [[Monthly Logs#📦 Log Archive|📦 Log Archive]]
