---
id: 314
title: 'courses.edx.org: PDF viewing, editing'
date: '2014-10-17T08:31:06+01:00'
author: Dave
layout: post
guid: 'http://www.monkeyandlamb.co.uk/itblog/?p=314'
permalink: /2014/10/courses-edx-org-pdf-viewing-editing/
categories:
    - Linux
tags:
    - linux
    - pdf
    - 'pdf editing'
    - 'pdf viewing'
format: aside
---

**Modifying PDFs with pdftk**

At times, you may want to merge, split, or rotate PDF files; not all of these operations can be achieved while using a PDF viewer. A great way to do this is to use the “PDF Toolkit”, **pdftk**, to perform a very large variety of sophisticated tasks. Some of these operations include:

- Merging/Splitting/Rotating PDF documents
- Repairing corrupted PDF pages
- Pulling single pages from a file
- Encrypting and decrypting PDF files
- Adding, updating, and exporting a PDF’s **metadata**
- Exporting bookmarks to a text file
- Filling out PDF forms

In short, there’s very little **pdftk** cannot do when it comes to working with PDF files; it is indeed the Swiss Army knife of PDF tools.

**Using pdftk**

You can accomplish a wide variety of tasks using **pdftk** including:

| **Command** | **Usage** |
|:-:|:-:|
| pdftk 1.pdf 2.pdf cat output 12.pdf | Merge the two documents 1.pdf and 2.pdf. The output will be saved to 12.pdf. |
| pdftk A=1.pdf cat A1-2 output new.pdf | Write only pages 1 and 2 of 1.pdf. The output will be saved to new.pdf. |
| pdftk A=1.pdf cat A1-endright output new.pdf | Rotate all pages of 1.pdf 90 degrees clockwise and save result in new.pdf**.** |

**Encrypting PDF Files**

If you’re working with PDF files that contain confidential information and you want to ensure that only certain people can view the PDF file, you can apply a password to it using the user\_pw option. One can do this by issuing a command such as:

$ pdftk public.pdf output private.pdf user\_pw PROMPT

When you run this command, you will receive a prompt to set the required password, which can have a maximum of 32 characters. A new file, private.pdf, will be created with the identical content as public.pdf, but anyone will need to type the password to be able to view it.

**Using Additional Tools**

You can use other tools, such as **pdfinfo**, **flpsed**, and **pdfmod** to work with PDF files.

**pdfinfo** can extract information about PDF files, especially when the files are very large or when a graphical interface is not available.

**flpsed** can add data to a PostScript document. This tool is specifically useful for filling in forms or adding short comments into the document.

**pdfmod** is a simple application that provides a graphical interface for modifying PDF documents. Using this tool, you can reorder, rotate, and remove pages; export images from a document; edit the title, subject, and author; add keywords; and combine documents using drag-and-drop action.

For example, to collect the details of a document, you can use the following command:  
$ pdfinfo /usr/share/doc/readme.pdf

**Converting Between PostScript and PDF**

Most users today are far more accustomed to working with files in PDF format, viewing them easily either on the Internet through their browser or locally on their machine. The PostScript format is still important for various technical reasons that the general user will rarely have to deal with.

From time to time you may need to convert files from one format to the other, and there are very simple utilities for accomplishing that task. **ps2pdf** and **pdf2ps** are part of the **ghostscript** package installed on or available on all Linux distributions. As an alternative, there are **pstopdf** and **pdftops** which are usually part of the **poppler** package which may need to be added through your package manager. Unless you are doing a lot of conversions or need some of the fancier options (which you can read about in the **man pages** for these utilities) it really doesn’t matter which ones you use.

Some usage examples:

| **Command** | **Usage** |
|:-:|:-:|
| pdf2ps file.pdf | Converts file.pdf to **file.ps** |
| ps2pdf file.ps | Converts**file.ps** to ****file.pdf**** |
| pstopdf input.ps output.pdf | Converts **input.ps to output.pdf |
| pdftops input.pdf output.pdf | Converts **input.pdf** to output.ps |