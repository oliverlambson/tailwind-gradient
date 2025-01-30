# tailwind-gradient bug reproduction

> For https://github.com/tailwindlabs/tailwindcss/issues/16037

## Running the reproduction

```sh
nvm use 22
npm i
npm run build:css # to generate styles.css
python -m http.server -d . # to serve files
```

## Details of the error

Inside the generated styles.css, grep for `from-blue-500` (I've formatted below for clarity):
```css
  .from-blue-500 {
    --tw-gradient-from: var(--color-blue-500);
    --tw-gradient-stops: var(
      --tw-gradient-via-stops,
      var(--tw-gradient-position,) /* missing comma after closing paren */
      var(--tw-gradient-from) var(--tw-gradient-from-position),
      var(--tw-gradient-to) var(--tw-gradient-to-position)
    );
  }
```

```diff
- var(--tw-gradient-position,)
+ var(--tw-gradient-position),
```
