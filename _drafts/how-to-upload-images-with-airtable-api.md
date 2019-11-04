---
layout: post
title: How to upload images with airtable api
subtitle: ''
gh-repo: marcomelilli
gh-badge:
- follow
tags: []
comments: true
date: 
published: false

---
\# **How to upload images with airtable api**

Airtable doesn’t allow you to directly upload attachments via their api. In the request we need to send the URL of the resource hosted in another server. In this way airtable can download the file and upload a copy in its server.

The easiest way I found for my projects is using \[Cloudbinary\]([https://cloudinary.com](https://cloudinary.com "https://cloudinary.com")) because it offers a generous free plan (25 monthly credits where 1 credit == 1GB of managed storage).

\## **Configure Cloudinary**  
 Todo

\## **Upload image with react-drop**  
 Todo