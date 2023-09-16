---
layout: post
read_time: true
show_date: true
title:  Compress input file images before upload 
date:   2022-11-14 13:32:20 -0600
description: Compress input file images before upload
img: posts/javascript_compress_image.jpg
tags: [javascript,vanilla]
author: Miguel García Domínguez
github:  MGDSoft/blog/
mathjax: yes
---

I've found an excellent library for compressing images before uploading them to the server. It's user-friendly and provides excellent compression.

Here's the link to the library: [browser-image-compression](https://github.com/Donaldcwl/browser-image-compression)

To use it in your project:

1. Install the library with npm or use the CDN.

```sh
npm install browser-image-compression --save
```

2. create this SIMPLE js file and copy where you want to use it.

```js
import imageCompression from 'browser-image-compression';
window.handleImageUpload = async (event) => {

  const imageFile = event.target.files[0];
  console.log('originalFile instanceof Blob', imageFile instanceof Blob); // true
  console.log(`originalFile size ${imageFile.size / 1024 / 1024} MB`);

  // see more options in the docs
  const options = {
    maxSizeMB: 10,
    maxWidthOrHeight: 1000,
    useWebWorker: true,
  }
  try {
    const compressedFile = await imageCompression(imageFile, options);
    console.log('compressedFile instanceof Blob', compressedFile instanceof Blob); // true
    console.log(`compressedFile size ${compressedFile.size / 1024 / 1024} MB`); // smaller than maxSizeMB

    // here is for replace the original file with the compressed one 😍
    let file = new File([compressedFile], imageFile.name,{type:imageFile.type, lastModified:new Date().getTime()});
    let container = new DataTransfer();
    container.items.add(file);
    event.target.files = container.files;

  } catch (error) {
    console.log(error);
  }

};
```
And in the html you have to call the function handleImageUpload when the input file change

```html
  <input type="file" accept="image/*" onchange="handleImageUpload(event)">
```

Easy peasy lemon squeezy. And please don't forget to buy a coffee to Donaldcwl he is a genious.
