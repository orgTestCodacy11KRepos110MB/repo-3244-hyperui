---
title: Tips & Tricks for Writing Better Tailwind CSS
slug: how-to-write-better-tailwindcss
date: 04/17/2022
emoji: 🧐
seo:
  title: How to Write Better Tailwind CSS
  description: I've been writing Tailwind CSS for since 2018 and have come across a few tips and tricks to make your code look and perform better.
---

Writing Tailwind CSS? Here are some tips and tricks that I apply when using Tailwind CSS to make my code look and perform better.

Got some tips to add to add? [Create a PR on GitHub](https://github.com/markmead/hyperui).

## Delegate Classes to Parent Element

### Incorrect

```
<ul>
  <li class="text-sm font-medium whitespace-nowrap">First</li>
  <li class="text-sm font-medium whitespace-nowrap">Second</li>
  <li class="text-sm font-medium whitespace-nowrap">Third</li>
</ul>
```

### Correct

```
<ul class="text-sm font-medium">
  <li class="whitespace-nowrap">First</li>
  <li class="whitespace-nowrap">Second</li>
  <li class="whitespace-nowrap">Third</li>
</ul>
```

---

## Remove Flex Classes on Mobile

### Incorrect

```
<div class="flex flex-col sm:flex-row sm:items-center sm:justify-between">
  <div>Hello</div>
  <div>World</div>
</div>
```

### Correct

```
<div class="sm:flex sm:items-center sm:justify-between">
  <div>Hello</div>
  <div>World</div>
</div>
```

---

## Evenly Space Content with Flow Root

### Incorrect

```
<ul class="space-y-8 divide-y">
  <li>First</li>
  <li class="pt-8">Second</li>
  <li class="pt-8">Third</li>
</ul>
```

### Correct

```
<div class="flow-root">
  <ul class="-my-8 divide-y">
    <li class="py-8">First</li>
    <li class="py-8">Second</li>
    <li class="py-8">Third</li>
  </ul>
</div>
```

> But this is more code

True, however...

- Which one will make more sense in a few months time?
- How would the first example work with dynamic content?

---

## Avoid Margin Bottom for Spacing Content

### Incorrect

```
<div>
  <div class="mb-4">Hello</div>
  <div>World</div>
</div>
```

### Correct

```
<div>
  <div>Hello</div>
  <div class="mt-4">World</div>
</div>
```

> What is the benefit, they do the same thing?

Sure, but what if the content is dynamic and there's no second element? You'll end up with extra space below the first element.

---

## Remove Duplicate Spacing Classes with Parent Classes

### Incorrect

```
<ul>
  <li>First</li>
  <li class="mt-8">Second</li>
  <li class="mt-8">Third</li>
</ul>
```

### Correct

```
<ul class="space-y-8">
  <li>First</li>
  <li>Second</li>
  <li>Third</li>
</ul>
```

---

## Use the Accurate Transition Class

### Incorrect

```
<button class="transition-all bg-red-500 hover:bg-red-600">Click</button>
```

### Correct

```
<button class="transition-colors bg-red-500 hover:bg-red-600">Click</button>
```

> But the class name is longer?

Can't argue with that, but do you need `transition-all`? Probably not.

**If you want to save on class name length then use `transition` it will cover
99% of the transition effects you need.**

---

## Use Color Opacity Classes

### Incorrect

```
<button class="relative">
  <span class="absolute inset-0 bg-red-500 opacity-50"></span>
  Click
</button>
```

### Correct

```
<button class="bg-red-500 bg-opacity-50">Click</button>
<!-- With JIT -->
<button class="bg-red-500/50">Click</button>
```

---

## Split CSS Class Names onto Multiple Lines in CSS Files

### Incorrect

```
<style>
  .button {
    @apply inline-flex items-center rounded border text-sm px-5 py-3 transition hover:scale-105;
  }
</style>
```

### Correct

```
<style>
  .button {
    @apply inline-flex items-center; // Layout
    @apply px-5 py-3 text-sm; // Spacing/Sizing
    @apply rounded border; // Style
    @apply transition; // Transition
    @apply hover:scale-105; // Interaction
  }
</style>
```

> How is this better? It's more code...

Correct, but it's easier to read and it all gets compiled down.

---

## Avoid Creating Components in CSS Files

**Only applies if you are using a templating language that allows for
components, such as Blade, React, Liquid OR Vue.**

### Incorrect

```
<div class="card">
  <div class="card-title">Title</div>
  <div class="card-body">Title</div>
  <div class="card-footer">
    <div class="card-timestamp">15/05/2025</div>

    <div class="card-actions">
      <button>Edit</button>
      <button>Delete</button>
    </div>
  </div>
</div>

<style>
  .card {
    @apply p-4 rounded;
  }

  .card-title {
    @apply text-lg;
  }

  .card-body {
    @apply mt-1;
  }

  .card-footer {
    @apply flex items-center justify-between;
  }

  .card-timestamp {
    @apply text-sm;
  }

  .card-actions {
    @apply flex gap-4;
  }
</style>
```

### Correct

```
<div class="p-4 rounded">
  <div class="text-lg">Title</div>
  <div class="mt-1">Title</div>
  <div class="flex items-center justify-between">
    <div class="text-sm">15/05/2025</div>

    <div class="flex gap-4">
      <button>Edit</button>
      <button>Delete</button>
    </div>
  </div>
</div>
```

---

## Use Max Width Classes When Restricting Width

### Inccrect

```
<div class="w-auto sm:w-64">
  <div>Hello World</div>
</div>
```

### Correct

```
<div class="max-w-sm">
  <div>Hello World</div>
</div>
```

> What's the benefit?

There's a few:

- They are responsive by default
- They better describe the layout

---

## Group Prefixed Class Names

### Incorrect

```
<div class="mt-4 text-lg sm:mt-0 sm:text-xl lg:text-3xl">
  Hello World
</div>
```

### Correct

```
<div class="mt-4 text-lg sm:mt-0 sm:text-xl lg:text-3xl">
  Hello World
</div>
```

You can use something like [Headwind](https://github.com/heybourn/headwind) to do this for you.

---

## Be Specific with Breakpoint Classes

### Incorrect

```
<div class="items-center justify-between sm:flex">
  <div>Hello</div>
  <div>World</div>
</div>
```

### Correct

```
<div class="sm:flex sm:items-center sm:justify-between">
  <div>Hello</div>
  <div>World</div>
</div>
```

> What's the issue here?

You are loading extra CSS on mobile that isn't being used. This might not seem drastic in this example but imagine the
whole frontend is written like the first example... That's a lot of extra CSS being loaded on mobile.

---

## Use Headwind and Tailwind CSS Intellisense

### Headwind

[GitHub Repo](https://github.com/heybourn/headwind)

- Sort Tailwind CSS class names
- Remove duplicate class names
- Move custom class names to end of class name list

### Tailwind CSS Intellisense

[GitHub Repo](https://github.com/tailwindlabs/tailwindcss-intellisense)

- Autocomplete Tailwind CSS class names (includes classes added in the Tailwind CSS config)
- Highlights errors with Tailwind CSS class names
- Displays the CSS generated with each Tailwind CSS class