
### Preface
<aside class='def'>
    <li>Shiny:  A web application framework in R.</li>
    <li>R:  An open-source programming language widely used in data-centric industries</li>
</aside>
This post documents how I turned solutions to data-wrangling problems using R and R shiny. Though the project is personal, I have a lot of fun watching my ideas turning into actually usable application.

### Problem Scope
A friend of mine complains about how much her job made her work overtime and the reason behind was some mind-numbingly copy-and-paste tables from an Excel worksheet to a Word document. 

These tables were called `labels`.  ^52ed22

| ![[Pasted image 20240121142513.png]] | ![[Pasted image 20240121144513.png]] |
| :--: | :--: |
| labels in Excels | labels in Word |
I told her all these work could be automated using R. In order to convert Excel labels into Word labels, we had to solve the following problems: 

> [!todo] Extract all the columns
> In Excel, the [[#^52ed22|labels]] were layouted next to one another in the worksheet: there is one label for every two columns in the entire table of the worksheet. ^d50ba3

> [!todo]
> For each described label above, wrote it into new page of a word document and a break after. 

>[!todo] 
>1. A set of specific formats were applied to each label, it can be achieved by calling VBA functions. 

> [!todo|bg-red]
> Paste the picture in the last row below the label if there was any. These can be achieved by using VBA functions. 
>
### Solution
All of the problems above can be solved using R and since you are reading this post, I am going to assume you are familiar with R and its IDE Rstudio. I am going to show you how you will be [[Working with Excel data in R]] using the `{readxl}` and `{openxlsx}` packages. Before we work our way to a production, let's begin with simple function.