---
Main Moc: "[[Tech MOC]]"
related:
  - "[[Quartz]]"
  - "[[My Quartz Setup Process]]"
completed: true
created: 2024-12-04T08:45
updated: 2025-04-13T15:06
---
>[!abstract] Related
>- [[My Quartz Setup Process]]
>- [[Quartz]]

---

### Adding an Icon to the Page Title

To add an icon to the page title, we need to edit the `PageTitle.tsx` component. The relative path to this file from the root is `quartz/components/PageTitle.tsx`.

![[Screenshot 2024-12-04 at 08.10.26.png|700]]

---
### Modified Code

Here's the modified code in `PageTitle.tsx`, with added comments to highlight the changes:

```TypeScript
import { pathToRoot } from "../util/path"
import { QuartzComponent, QuartzComponentConstructor, QuartzComponentProps } from "./types"
import { classNames } from "../util/lang"
import { i18n } from "../i18n"

const PageTitle: QuartzComponent = ({ fileData, cfg, displayClass }: QuartzComponentProps) => {
  const title = cfg?.pageTitle ?? i18n(cfg.locale).propertyDefaults.title    
  const baseDir = pathToRoot(fileData.slug!)
  return (
    <h2 class={classNames(displayClass, "page-title")}>
      <img src="/static/icon.png" alt="icon" class="icon" />   // added (icon + use you file path here)
      <a href={baseDir}>{title}</a>
    </h2>
  )
}

PageTitle.css = `
.page-title {
  font-size: 2.2rem;         //modified (increased font)
  margin: 0;
  display: flex;             //added
  align-items: center;       //added
  justify-content: center;   //added
}

.page-title .icon {          //added 
  margin-right: 0.5rem;      //added (right padding) 
  width: 60px;               //added (icon size - change to fit your needs)
  height: 60px;              //added (icon size - change to fit your needs)
}                            //added
`

export default (() => PageTitle) satisfies QuartzComponentConstructor
```

When adding the icon, make sure to update the `src` attribute with the correct file path. If the icon is already on your site, use the relative path as shown in the example. If you want to use a new icon, you have two options:

* Use a URL if the image is hosted online (e.g., `src="https://via.placeholder.com/24"`).
* Add the image to your site (e.g., in the `/static` folder) and use the relative path in the code (e.g., `src="/static/your_custom_icon.png"`).