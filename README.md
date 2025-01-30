# tailwind-gradient bug reproduction

```sh
nvm use 22
npm i
npm run build:css # to generate styles.css
python -m http.server -d . # to serve files
```

generated code
```css
.from-blue-500 {
  --tw-gradient-from: var(--color-blue-500);
  --tw-gradient-stops: var(
    --tw-gradient-via-stops,
    var(--tw-gradient-position,) var(--tw-gradient-from) /* missing comma after gradient position */
      var(--tw-gradient-from-position),
    var(--tw-gradient-to) var(--tw-gradient-to-position)
  );
}
.to-green-500 {
  --tw-gradient-to: var(--color-green-500);
  --tw-gradient-stops: var(
    --tw-gradient-via-stops,
    var(--tw-gradient-position,) var(--tw-gradient-from) /* missing comma after gradient position */
      var(--tw-gradient-from-position),
    var(--tw-gradient-to) var(--tw-gradient-to-position)
  );
}
```

correct code
```css
.from-blue-500 {
  --tw-gradient-from: var(--color-blue-500);
  --tw-gradient-stops: var(
    --tw-gradient-via-stops,
    var(--tw-gradient-position,), var(--tw-gradient-from)
      var(--tw-gradient-from-position),
    var(--tw-gradient-to) var(--tw-gradient-to-position)
  );
}
.to-green-500 {
  --tw-gradient-to: var(--color-green-500);
  --tw-gradient-stops: var(
    --tw-gradient-via-stops,
    var(--tw-gradient-position,), var(--tw-gradient-from)
      var(--tw-gradient-from-position),
    var(--tw-gradient-to) var(--tw-gradient-to-position)
  );
}
```
