---
title: "Good Document Titles Don't Just Help Humans — They Help Your RAG Pipeline Too"
date: 2026-03-15
draft: false
summary: "A naming convention I built for a SharePoint knowledge base in 2009 turns out to be exactly what modern RAG pipelines need too."
tags: ["knowledge-management", "rag", "sharepoint", "ai-tools", "documentation"]
categories: ["Solutions"]
---

Back in 2009 I implemented a knowledge management system at GHD Engineering in Brisbane using Windows SharePoint Services. Within six months, IT staff across multiple offices were actively referencing the wiki knowledge base.

## What Made It Work

I attribute the wiki's success to four things:

1. A logical naming convention for articles
2. A structured article body format
3. Ongoing maintenance of the hierarchical page organisation
4. Management support and advocacy

## The Naming Convention Problem

Generic summarisation approaches create problems fast. When every article is labelled something vague, a search for "out of office" yields a list of articles your eyes have to painstakingly scan through.

I developed a **top-down chunking approach** with four hierarchical levels:

- **1st Level:** Category (Software, Hardware, Network)
- **2nd Level:** Brand (Microsoft, Dell, Cisco)
- **3rd Level:** Product Name/Version (Outlook 2010, Optiplex 7700)
- **4th Level:** Article Type (Error, Issue, How To)

**Examples:**
- Software - Microsoft - Outlook 2010 - How To - Recover Deleted Items
- Software - Microsoft - Outlook 2010 - Error - Cannot start Microsoft Outlook
- Software - Microsoft - Outlook 2010 - Issue - Hyperlinks not working

## Article Body Structure

I implemented a simple template-based system:

- **First Heading:** HOW TO, ERROR, or ISSUE
- **Second Heading:** SOLUTION

Content varied by article type and included procedural steps, error descriptions, screenshots, and technical explanations. Each article automatically displayed author, modification date, and breadcrumb navigation.

## Addressing Contributor Hesitation

Some staff hesitated to contribute directly due to concerns about proper placement and format adherence. I addressed this by personally managing article submissions — prioritising content capture over structural perfection.

The same principle applies directly to RAG pipelines today. Clear, structured titles make retrieval dramatically more accurate. The discipline is the same; only the technology has changed.
