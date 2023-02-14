---
layout: default
title: Image Optimization
parent: SEO
grand_parent: General
nav_order: 2
---

# Image Optimization
{: .no_toc}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### Introduction
This document outlines an optimised image naming convention for e-commerce sites. This convention allows images to be bulk imported and exported from the site.

### Image Specification
- File type: JPG
- Optimum size: 1200px by 1200px
- Target file size: 80~150kb (we can compress on upload)
- Image variations (each product should have as many of these variations as possible):
    - Product on what background (Google Shopping)
    - Product with brand logos
    - Product with the key spec (size/features)
    - The product being used in-situ

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