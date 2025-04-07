---
created: 2025-01-01T21:51
updated: 2025-04-07T09:59
tags:
  - monthly-log
---
## Video games worth of enjoying

Since I was little, I’ve always had a passion for playing video games. However, university brought a much busier and more strict schedule, making it hard to dedicate time to “wasteful” activities like gaming.

I understood that things were becoming unhealthy when even the thought of choosing my next game turned into a stressful decision, as my mind stared thinking of all the other,  more productive things I could be doing.

To overcome this, I started exploring smaller and simpler games, that require less time and commitment. This not only allowed me to enjoy gaming sacrificing less precious hours, but also made me possible to discover "hidden" gems from independent studios. These games, are seen to stupid ape brain as *small work of art worth of enjoying*.

For example, this month I played [Planet of Lana](https://planetoflana.com) a crazy beautiful, story driven, short puzzle game characterized by a cozy visual style that brings to mind the films form [Studio Ghibli](https://en.wikipedia.org/wiki/Studio_Ghibli "Studio Ghibli"), which can be enjoyed in less that 5 hours. 

![[planet_of_lana_image.webp]]

>This game screen shots are taken from steam reviews of the game, I wanted to use to use my own screenshots but I lost the save files :(

## 🌐 Site Update

The pages of this site are just [markdown]() files that I write using [obsidian](https://obsidian.md/), than I use a tool called [quartz](https://quartz.jzhao.xyz/) to convert my obsidian vault in this static website. 

There are different ways to make a site using quartz depending on the platform you want to use to host your site but the simplest and cheapest (it' free) way is to use GitHub, so that's what I did. The easiest and fastest way to set up quartz using Github it's just to clone the quartz official repo and than paste your obsidian vault inside the content directory. This is really easy to set up but it means that each time you want to update you content you have to manually copy and paste you vault in the content directory.

But I like automating things so I decided to use two separate repos one for quartz and one for the obsidian vault and than I created a submodule inside the content directory that links to the vault repo. This meant that I didn’t have to manually copy and paste the vault but I just had to run a command onside the quartz repo that updates the submodule.

```bash
git submodule update --remote content/vault
```

This is how I have always updated my site content, but there is not fully autonomous because I still had to open the terminal write the commands and push the changes. So this month I spend some time learning about git submodules, Github secrets and actions and I have been able to use this things to completely automate the site content update. Now each time I push the changes of my obsidian vault to Github the quartz repo is notified about the change and *automagicaly* updates all the submodules. If you want to learn how to do this, I have written a [[Using GitHub Actions to automatically update repo's submodules|small guide]].

---

>**See all the other monthly logs:** [[Monthly Logs#📦 Log Archive|📦 Log Archive]]

