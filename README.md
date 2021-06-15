# Background
[ZN Studio](https://znstudio.com.au) is a digital experience design consulting studio in Brisbane with a goal to contribute our share of memorable experiences to this world. Every website, app and experience is designed, tested and built for the sake of this vision. Seriously, imagine a world where experience is always focused.

# Setup
```
npm install
npm run dev
```

# Technology

PostCSS should be used with the following plugins:

1. PostCSS Nested (https://github.com/postcss/postcss-nested)
2. TailwindCSS (https://tailwindcss.com)
3. Autoprefixer (https://github.com/postcss/autoprefixer)
4. PurgeCSS (https://purgecss.com/plugins/postcss.html#installation)

# Project Structure

1. Styles should be broken up into individual styles for understandability

```
styles
│   styles.css
│   scaffolding.css
│   helpers.css
│   fonts.css
│
└───components
    │   header.css
    │   footer.css
```

# Files

## styles.css

```
@import "fonts";
@import "scaffolding";
@import "helpers";
@import "typography";
@import "components/header";
@import "components/footer";
```

## fonts.css

Use this to declare any font faces, e.g.

```
@font-face {
  font-family: 'Neue Haas Grotesk Regular';
  src: url('../fonts/neue-haas-grotesk-regular.woff2') format('woff2'),
       url('../fonts/neue-haas-grotesk-regular.woff') format('woff');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}
```

## scaffolding.css

Use this to import Tailwind base and utility helpers, then basic setup;

```
@tailwind base;
@tailwind utilities;

html {
  @apply font-body;
  font-size: calc(100vw / 750 * 10);

  @screen sm {
    font-size: calc(100vw / 1920 * 10);
  }
}
```

## helpers.css

Useful in creating helper classes that are:

1. General in nature
2. Often extended by other components

For example a section component:

```
.section {
  @apply py-12;
  @screen sm {
    @apply py-24;
  }
}
```

This class might be extended by other components:

```
// component.css

.component {
  @apply section;
}

```

## typography.css

Used to create type classes that are extended by other components, at the end these are given to default h1, h2, h3 etc.

```
.h1 {
  @apply text-4xl;
  @apply font-bold;
}

h1 {
  @apply h1;
}
```

These classes can also be extended by components later,

```
// component.css

.heading-component {
  @apply h1;
}
```

# Code Guidelines

1. Extend TailwindCSS functionality rather than create custom code
2. Always @apply classes where possible, do not create custom styles if not necessary
3. Refactor complex components into component files
4. Use Tailwind `screen` directive over media queries
5. Nest CSS for readability, including media queries
6. Use BEM Syntax when creating custom component
7. Add `apply` values on new lines
8. Always use `rem` instead of `px`

## 1. Extend TailwindCSS functionality rather than create custom code
When deciding what tailwind classes to use, choose spacing and font sizes which are close, or create a new spacing within the tailwind config.

**✅ DO:**

```
module.exports {
  ...
  theme: {
    fontSize: {
      2xl: '10 rem'
    }
  }
}
```

```
type.css

.h4 {
  @apply text-2xl;
}
```

**❌ DON'T:**

```
.new-title {
  font-size: 10rem;
}
```

## 2. Always @apply classes where possible, do not create custom styles if not necessary

**✅ DO:**

```
// component.css

.component {
    @apply pt-4;
}
```

**❌ DON'T:**

```
.mobpt2 {
    padding-top: 2rem;
}
```

## 3. Refactor complex components into component files

**✅ DO:**

```
// component.css

.component {
    @apply pt-4;
    @apply mt-2;
    @apply w-full;
    @apply h-full;
    @apply text-lg;
    @apply text-base;
    @apply font-bold;
}
```

**❌ DON'T:**

```
// index.html

<div class="pt-4 mt-2 w-full h-full text-lg text-base font-bold">Name</div>
<div class="pt-4 mt-2 w-full h-full text-lg text-base font-bold">Name</div>
<div class="pt-4 mt-2 w-full h-full text-lg text-base font-bold">Name</div>
<div class="pt-4 mt-2 w-full h-full text-lg text-base font-bold">Name</div>
```

## 4. Use Tailwind `screen` directive over media queries

**✅ DO:**

```
// component.css

.component {
    @apply text-lg;
    @screen sm {
        @apply text-2xl;
    }
}
```

**❌ DON'T:**

```
// component.css

.component {
    @apply text-lg;
}

@media (min-width: 768px) {
    @apply text-2xl;
}
```

## 5. Nest CSS for readability, including media queries

It makes it really difficult to read if you don't nest.

**✅ DO:**

```
// component.css

.component {
    @apply text-lg;
    @screen sm {
        @apply text-2xl;
    }

    &__block {
        @apply bg-black;
        @apply text-white;
    }
}
```

**❌ DON'T:**

```
// component.css

.component {
    @apply text-lg;
}

@screen sm {
    .component {
        @apply text-2xl
    }
}

.component__block {
    @apply bg-black;
    @apply text-white;
}
```

## 6. Use BEM Syntax when creating custom component

**✅ DO:**

```
// component.css

.component {
    @apply text-lg;

    &__block {
        @apply bg-black;
    }

    &__block__another {
        @apply bg-orange;
    }
}
```

**❌ DON'T:**

```
// component.css

.component {
    @apply text-lg;

    & ul {
        @apply bg-black;
    }
}
```

## 7. Add `apply` values on new lines

This just helps readability of components, especially when lots of styles.

**✅ DO:**

```
// component.css

.component {
    @apply text-lg;
    @apply bg-black;
}
```

**❌ DON'T:**

```
// component.css

.component {
    @apply text-lg bg-black;
}
```

# Example Tailwind Config

```
const colors = require('tailwindcss/colors')

module.exports = {
  purge: {
    enabled: true,
    content: ['./**/*.html'],
  },
  darkMode: false, // or 'media' or 'class'
  theme: {
    colors: {
      transparent: 'transparent',
      flamingo: '#EF5B2F',
      serenade: '#FFF0E2',
      'black-haze': '#F0F1F1',
      manatee: '#9A9C9F',
      shark: '#272729',
      orange: '#F59331',
      black: colors.black,
      white: colors.white,
    },
    fontFamily: {
      display: ['divenire', 'sans-serif'],
      body: ['halcom', 'sans-serif'],
    },
    fontSize: {
      sm: '1.8rem',
      rg: '2rem',
      base: '2.2rem',
      lg: '2.6rem',
      xl: '2.8rem',
      xxl: '3.2rem',
      '2xl': '6.6rem',
      '3xl': '9.1rem',
      '4xl': '10rem',
      '5xl': '19rem',
    },
    spacing: {
      px: '1px',
      0: '0px',
      0.5: '0.25rem',
      1: '0.4rem',
      1.5: '0.750rem',
      2: '1rem',
      2.5: '1.25rem',
      3: '1.5rem',
      3.5: '1.75rem',
      4: '2rem',
      5: '2.5rem',
      6: '3rem',
      7: '3.5rem',
      8: '4rem',
      9: '4.5rem',
      10: '5rem',
      11: '5.5rem',
      12: '6rem',
      14: '7rem',
      16: '8rem',
      20: '10rem',
      24: '12rem',
      28: '14rem',
      32: '16rem',
      36: '18rem',
      40: '20rem',
      44: '22rem',
      48: '24rem',
      52: '26rem',
      56: '28rem',
      60: '30rem',
      64: '32rem',
      72: '36rem',
      80: '40rem',
      96: '48rem',
    },
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
}

```

# 8. Always use `rem` instead of `px`
Styling should always be in `rem` values as they are relative to the body font size, which changes based on the screen width.

This means that every element will by, default, scale up and down as the window changes.

Furthermore, the calculations on the body means that any pixel value from a design can be easily converted into an equivalent `rem` in the code.

For example,
A `120px` padding at the top of an element, would be equivalent to `12rem` in this system. This is helpful in determining the `rem` value.

**✅ DO:**

```
// component.css

.component {
  margin-top: 10rem;
}
```

**❌ DON'T:**

```
// component.css

.component {
    margin-top: 100px;
}
```


# Visual Studio Code Extensions
Highly recommended that you use this: https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss

Follow install instructions.

