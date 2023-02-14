---
layout: default
title: Best Practices
parent: SEO
grand_parent: General
nav_order: 6
---

# Best Practices
{: .no_toc}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### Introduction
This document outlines some best practices for common situations that can bring down SEO rankings in websites.

### Multiple H1 tags
Multiple H1 tags bring down SEO ranking, this should be avoided. It can be identified and resolved in the following steps;
1. Right click on any space on the webpage. From the menu, select "View Page Source".
2. On the page source, using "Ctrl (or command) + F", search for "h1".
3. The texts that have the "h1" tag is then visible to be taken care of.
4. If the texts can only be edited from the codebase, contact the developer to resolve.

### Image Naming
- Images should be named using the product SKU they are associated with. These should only use lowercase letters and numbers and prepended with a hyphen, followed by an ascending number starting at zero. I.e for a product with a SKU of: TAP112233, images would be saved as:
    - tap112233-0.jpg (always used as the featured thumbnail)
    - tap112233-1.jpg
    - tap112233-2.jpg
    - tap112233-3.jpg
    - tap112233-4.jpg
    - tap112233-9.jpg (used for Google Shopping feed)

- For variational products (products with options) we recommend a SKU convention that inherits the parent SKU followed by an identified.i.e. TAP112233-001, TAP112233-002. The images for these products would be:
    - tap112233-001-0.jpg (always used as the featured thumbnail)
    - tap112233-001-1.jpg
    - tap112233-001-2.jpg
    - tap112233-001-9.jpg (used for Google Shopping feed)
    - tap112233-002-0.jpg (always used as the featured thumbnail)
    - tap112233-002-1.jpg
    - tap112233-002-2.jpg
    - tap112233-002-9.jpg (used for Google Shopping feed)

### Folder Structure
All images should be saved in a single folder (no subfolders). This makes it easy to spot missing images and also means the import process can look at a single directory for all image files.