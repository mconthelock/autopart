# Get start Nuxt3

## Initial Project

```bash
npx nuxi init <projectname>
npm install
```

---

## Install Tailwin

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

_Add Tailwind to your PostCSS configuration in nuxt.config.js_

```javascript
postcss: {
    plugins: {
        tailwindcss: {},
        autoprefixer: {},
    }
}
```

_Configure your template paths in tailwind.config.js file_

```javascript
module.exports = {
  mode: "jit",
  content: [
    "./components/**/*.{js,vue,ts}",
    "./layouts/**/*.vue",
    "./pages/**/*.vue",
    "./plugins/**/*.{js,ts}",
    "./nuxt.config.{js,ts}",
    "./app.vue",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

_Create file css at assets/css/style.css and add the Tailwind directives to style.css_

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

_Start build process_

```bash
npm run dev
```

---

## Install @nuxtjs/robots support SEO

```bash
npm install @nuxtjs/robots -D
```

_Config nuxt.config.ts for Meta SEO Tag_

```javascript
modules: [
    [// Nuxt Robots
        '@nuxtjs/robots',
        {
          UserAgent: "*",
          Disallow: "",
        }
    ],
],
app: {
    head: {
        htmlAttrs: {
            lang: 'en'
        },
        bodyAttrs: {
            class: 'demo'
        },
        charset: 'utf-8',
        titleTemplate: '%s | My app',
        meta: [
            {
                name: 'author',
                content: 'onthelock'
            },
            {
                name: 'viewport',
                content: 'width=device-width, initial-scale=1, maximum-scale=5'
            }
        ],
         link: [
            {
                rel: "stylesheet",
                href: "https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@200;300;400;500;600;700&family=Inter:wght@200;300;400;500;600;700;800;900&display=swap",
            },
            {
                rel: "icon",
                type: "image/x-icon",
                href: "/favicon.ico"
            }
        ],
    }
},
```
