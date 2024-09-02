---
dg-publish: true
dg-home: true
sticker: lucide//blinds
color: var(--mk-color-turquoise)
---


## Index of All Files and Folders


```dataviewjs
// Fetch all pages (files and folders) from the vault
let pages = dv.pages("").sort(p => p.file.folder, 'asc');

// Group the pages by their folder paths
for (let group of pages.groupBy(p => p.file.folder)) {
    // Display the folder name as a heading, with "Root" renamed to "Home"
    let folderName = group.key || "Home"; // Replace "Home" with whatever you want to call the root
    dv.header(3, folderName);

    // Sort the files within the folder and list them first
    let files = group.rows.filter(p => !p.file.folder).sort(p => p.file.name, 'desc');
    dv.list(files.map(p => `[[${p.file.name}]]`));

    // Then, list the subfolders within the folder
    let folders = group.rows.filter(p => p.file.folder).sort(p => p.file.name, 'desc');
    dv.list(folders.map(p => `[[${p.file.name}]]`));
}
```





[[Countries]] 