---
parent: CSS
nav_order: 5
---

# Tailwind CSS

Tailwind is an interesting twist on the usual css frameworks like bootstrap. Instead of giving you a lot of pre-built blocks and components, it just gives you tons of utility classes. In css frameworks like bootstrap, you often have to override the css component classes to incorporate your design. Not in tailwind: you don't get component classes at all, just utility classes. Idea is to never write css at all. Let me show what I mean.
[Reference 1](https://tsh.io/blog/tailwind-css-tutorial/).
[Reference 2](https://scotch.io/tutorials/get-started-with-tailwind-css-in-15-minutes).

```html
<div class="bg-green-300 border-green-600 border-b p-4 m-4 rounded">
  Hello World
</div>
```

Will result in

![](https://tsh.io/wp-content/uploads/2021/03/tailwind-css-hello-world_.png)

Here's what each of the above classes mean:

- `bg-green-300`: green background with shade 300
- `border-green-600`: green border with higher shade
- `border-b`: set border visible at bottom
- `p-4 m-4`: padding and margin of 4 units
- `rounded`: rounded corners

So, you make your own components by pulling together different utility classes from tailwind. Let me contrast this with how bootstrap does stuff. Here's how create a card in bootstrap:

```html
<div class="card" style="width: 18rem;">
  <div class="card-body">
    <h5 class="card-title">Card Title</h5>
    <p class="card-text">Content goes here</p>
  </div>
</div>
```

![](https://scotch-res.cloudinary.com/image/upload/dpr_2,w_800,q_auto:good,f_auto/v1582133740/wynfxsgsd0dfvhf8nltl.png)

But in tailwind, you have:

```html
<div class="bg-white rounded shadow border p-6 w-64">
  <h5 class="text-3xl font-bold mb-4 mt-0">My Title</h5>
  <p class="text-gray-700 text-sm">Content goes here</p>
</div>
```

![](https://scotch-res.cloudinary.com/image/upload/dpr_2,w_800,q_auto:good,f_auto/v1582133748/wkeppbh1yvrn2jpremkn.png)

You may argue bootstrap code looks cleaner and better. But you're stuck to bootstrap's default design unless you go into overriding the css classes, which is easier said than done. On the other hand, in tailwind, you get your _own_ card without editing any css! In other words, bootstrap is design-opinionated while tailwind is design-odor free.

Doesn't this make your html look busy? Yep. But does it matter? Probably not because you're using a framework like react where you write your component only once. There are [other tricks](https://tailwindcss.com/docs/utility-first#maintainability-concerns)), but I'll not get into them

```js
function MyCard() {
  return (
    <div class="bg-white rounded shadow border p-6 w-64">
      <h5 class="text-3xl font-bold mb-4 mt-0">My Title</h5>
      <p class="text-gray-700 text-sm">Content goes here</p>
    </div>
  );
}
```

What if you want to customize the font or colors? You just specify your [theme](https://tailwindcss.com/docs/theme) in one place at `tailwind.config.js`. Here's how it can look like

```js
// tailwind.config.js
const colors = require("tailwindcss/colors");

module.exports = {
  theme: {
    screens: {
      sm: "480px",
      md: "768px",
      lg: "976px",
      xl: "1440px",
    },
    colors: {
      gray: colors.coolGray,
      blue: colors.lightBlue,
      red: colors.rose,
      pink: colors.fuchsia,
    },
    fontFamily: {
      sans: ["Graphik", "sans-serif"],
      serif: ["Merriweather", "serif"],
    },
    extend: {
      spacing: {
        128: "32rem",
        144: "36rem",
      },
      borderRadius: {
        "4xl": "2rem",
      },
    },
  },
};
```

You can add interaction too quite easily by using prefixing your classes with css pseudoselector like hover.

```html
<div class="bg-gray-500 hover:bg-red-600 ..."></div>
```

![](https://tsh.io/wp-content/uploads/2021/03/tailwind-css-hover_.png)

How about responsiveness? Just add prefixes of sizes `sm`/`md` etc.

```html
<div class="m-2 sm:m-4 md:m-8 lg:m-16 xl:m-32"></div>
```

Here, margin will change based on the screen size.

Because there are so many classes in tailwind, tailwind css can be very big. But then you don't have to include classes you didn't use in your build. Follow installation instructions in the [website](https://tailwindcss.com/docs/installation) to setup for your specific stack.
