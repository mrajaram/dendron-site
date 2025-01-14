---
id: LAUb8WcM8rmjxJrR
title: Arch
desc: ''
updated: 1636389281294
created: 1627859879590
---

## Summary

You can see a video walkthrough of how we generate notes for publishing and the static export [here](https://youtu.be/Uyyb_s74lzM)

## Components
<!-- Major components -->

## Lifecycle
- building metadata
  - `dendron publish build`
  - dendron will look at your `dendron.yml`
  - generate metadata into json files
  - [NextJsExportPod](https://github.com/dendronhq/dendron/blob/68fea3bbad13961b7754e61dd63dfb2d47d73c56/packages/pods-core/src/builtin/NextjsExportPod.ts#L30)
- building the site

### Startup

What happens when you visit a statically generated Dendron site. 

- pages/_app.tsx

- see generated asset files in [[References|dendron://dendron.dendron-site/dendron.topic.pod.builtin.nextjs#references]]
```tsx
DendronApp {

  useEffect {
    data = fetchNotes { fetch("/data/notes.json") }
    setNoteData data
    fetchConfig { fetch("/data/dendron.json") }
  }
}
```

- components/DendronNotePage.tsx

```tsx
Note {
  id = getActiveNoteId

  ...
}
```

## Publishing

This describes how notes are filtered for publishing

- src/builtin/NextjsExportPod.ts
```ts
SiteUtils.filterByConfig 
```

### filterByConfig

```ts
siteHierarchies := sconfig

hiearchiesToPublish = 
```

### filterByHiearchy

```ts
filterByHiearchy(domain, notes) {
  hconfig := getConfigForHierarchy

  notes = notesGet(domain, notes)
  if notes.length > 1 {
    domainNote = handleDup(...)
  } else {
    domainNote = notes[0]
  }

  ...
  processQ = [domainNote]
  while processQ {
    note = processQ.pop
    maybeNote = filterByNote(note)
    if (!maybeNote) return;

    children = getChildren(maybeNote)
    ...
    children.filter(canPublish)!

    children.forEach { 
      processQ.push it
    }


  }
}
```

### home page
The `index` page is generated from the [[noteIndex|pkg.nextjs-template.arch.nextjs-pod#noteindex]] of the nextjs pod.