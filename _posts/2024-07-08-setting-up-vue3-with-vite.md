---
layout: post
title: "Setting up Vue3 project fith Vite and some additional stuff"
date: 2024-07-08 14:00:00 +0100
categories: vue3 vite tailwind daisyUI VuesticUI
---

Recently I've started playing around with Vue3.

First I had to install node. I did that on Windows with nvm (node version manager) and use node v22.

I have found numerous tutorials, however not everything in them worked out for me.

This is what I use to setup new project and so far works:

{% highlight bash %}
npm create vite@latest
{ endhighlight }

I select name of the project and then select framework as Vue3 + TypeScript.

After creating it, I can confirm it works with:

{% highlight bash %}
cd name-of-my-project
npm install
npm run dev
{ endhighlight }

At this stage it should work. One weird quirk is it will never work when I'm in a directory that is a junction link, or contains ! in it's path.

After that I either install Tailwind + daisyUI or VuesticUI.

Tailwind + daisyUI: [How to add Tailwind DaisyUI In Vue 3 - webvees](https://webvees.com/post/how-to-install-tailwind-daisyui-in-vue-3/)

VuesticUI: I use "manual installation" from [https://ui.vuestic.dev/getting-started/installation](https://ui.vuestic.dev/getting-started/installation)