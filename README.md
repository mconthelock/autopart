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

1. Add Tailwind to your PostCSS configuration in nuxt.config.js

```javascript
postcss: {
    plugins: {
        tailwindcss: {},
        autoprefixer: {},
    }
}
```

2. Configure your template paths in tailwind.config.js file

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

3. Create file css at assets/css/style.css and add the Tailwind directives to style.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

4. Start build process

```bash
npm run dev
```

---

## Install @nuxtjs/robots and Config nuxt.config.ts file to support SEO

```bash
npm install @nuxtjs/robots -D
```

Config nuxt.config.ts for Meta SEO Tag

```typescript
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

## Nuxt3 and Vuetify

1. After init nuxt project add 2 more depencies

```bash
npm install -D sass
npm install -D vuetify
npm install vite-plugin-vuetify
npm install -D nuxt-icon
npm install -D @nuxtjs/google-fonts
npm install -D @nuxtjs/robots
```

2. Create assets/scss/style.scss

```css
@use "vuetify/styles";
```

3. Config nuxt.config.ts

```typescript
import vuetify from "vite-plugin-vuetify";
export default defineNuxtConfig({
  ssr: true,
  css: ["@/assets/scss/style.scss"],
  build: {
    transpile: ["vuetify"],
  },
  vite: {
    ssr: {
      noExternal: ["vuetify"],
    },
    define: {
      "process.env.DEBUG": false,
    },
  },
  modules: [
    "nuxt-icon",
    [
      "@nuxtjs/robots",
      {
        UserAgent: "*",
        Disallow: "",
      },
    ],
    // this adds the vuetify vite plugin
    // also produces type errors in the current beta release
    async (options, nuxt) => {
      // @ts-ignore
      nuxt.hooks.hook("vite:extendConfig", (config) =>
        config.plugins.push(vuetify())
      );
    },
  ],
  app: {
    head: {
      htmlAttrs: {
        lang: "en",
      },
      bodyAttrs: {
        class: "demo",
      },
      charset: "utf-8",
      titleTemplate: "%s - Nuxt 3 Vuetify",
      meta: [
        {
          name: "viewport",
          content: "width=device-width, initial-scale=1, maximum-scale=5",
        },
        {
          name: "author",
          content: "IT Genius Engineering Ltd., Thailand",
        },
      ],
    },
  },
});
```

4. Create plugins/vuetify.ts

```typescript
// import createVuetify from "vuetify"
import { createVuetify } from "vuetify"; //init step

// import custom icons from helpers
import { aliases, custom } from "@/helpers/customIcons";

// import theme from "@/helpers/themes"
import {
  LIGHT_THEME,
  lightTheme,
  DARK_THEME,
  darkTheme,
} from "@/helpers/themes";

// import defaults from "@/helpers/defaults"
import { defaults } from "@/helpers/defaults";

export default defineNuxtPlugin((nuxtApp) => {
  // Create a new Vuetify instance
  const vuetify = createVuetify({
    //init step
    ssr: true, //init step
    defaults,
    theme: {
      defaultTheme: LIGHT_THEME,
      themes: {
        lightTheme,
        darkTheme,
      },
      // add color variations
      variations: {
        colors: ["primary", "secondary"],
        lighten: 3,
        darken: 3,
      },
    },
    // Add the custom iconset
    icons: {
      defaultSet: "custom",
      aliases,
      sets: {
        custom,
      },
    },
  }); //init step

  // Inject it to nuxtApp
  nuxtApp.vueApp.use(vuetify); //init step
});
```
