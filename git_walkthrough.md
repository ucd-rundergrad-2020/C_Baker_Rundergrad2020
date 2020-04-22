---
title: "Git Upload Walkthrough"
author: "Cassandra"
date: "4/22/2020"
output: 
  html_document: 
    keep_md: yes
---

## How do I upload my notes/homework to Github?

1. Create an R markdown file  
    * Click the page with the green plus located below `File`   
    * Select `R Markdown`  
    * Give your new file an informative title  
        * The title will show up at the top of your document, but is different from the file name  
    * Save your new file and give it an informative file name (no spaces!)     
2. Fill in your document  
    * Delete the default text except for the header (denoted by `---`)  
    * Include notes or interesting pieces of code from the book   
    * Include the assigned questions and your answers/attempts   
3. Prepare your document to be uploaded   
    * Click the `Settings` gear for your file  
        * Located at the end of icons on the top left of your file, next to the blue knit button   
    * Select `Output Options` and then the `Advanced` tab   
    * Check the box next to "Keep markdown source file"   
    * Knit the document by clicking `Knit` (with the blue ball of yarn)    
      * If it knits properly, you should see the rendered version of your document pop up in a separate R window   
      *  You can also see the knitting progress in your `R Markdown` tab (mine is in the same pane as the `Terminal`)   
    * Look through your document to make sure everything formatted as you intended    
4. Upload to Github   
    * In the `Git` tab of R Studio, check the boxes next to all files you'd like to upload   
      * R markdown file (.Rmd)   
      * Markdown file (.md)   
      * Html for completeness (.html)   
      * **Any figures produced in your document (.png)**   
    * Click `Commit` 
    * Write an informative commit message in the top right box of the window that pops up   
    * Select `Commit` underneath your commit message   
    * Once committed, select the green arrow `Push`   
5. Check your upload   
    * Open Github from your web browser   
    * Navigate to your repository   
    * View the .md file that you just pushed  
      * Does the format look good?   
      * Do you see your graphs?   
    
## Other tips and tricks     

### Shortcuts   

* For a new R code chunk press `Ctrl` + `Alt` + `i`    
  **Note:** For Macs, replace `Ctrl` with `Command`    
* For assignment operator `<-` press `Alt` + `-`     

**Is your file taking forever to knit because there are so many graphs in it?**    
You can include the below code at the beginning of your document to cache your file each time you knit, thus saving time on future knits because it doesn't have to remake the entire document every time.    
```
knitr::opts_chunk$set(cache = TRUE, autodep = TRUE)
```

### R chunk options   

1. Don't want a piece of code to show up in your final document? Use `include = FALSE` in the chunk options (so it looks like `{r include = FALSE}`).   
  **For this class, use sparingly.** I only do this for document setup options, such as the above `knitr` line.  

2. Tired of seeing messages in your final document? Use `message = FALSE` in the chunk options, as above.  
  This is great for loading packages so you don't have to see all the loading notes in your document.    
