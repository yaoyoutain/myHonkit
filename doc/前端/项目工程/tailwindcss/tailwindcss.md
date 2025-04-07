# tailwindcss

```bash title="安装"
npm install -D tailwindcss@3.4.17 postcss autoprefixer
npx tailwindcss init -p


```


```bash title="tailwind.config.js"
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```


```bash title="style.css"
@tailwind base;
@tailwind components;
@tailwind utilities;
```
