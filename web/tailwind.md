# [tailwindcss](https://tailwindcss.com/)

## Activating variants not active by default

- Modify tailwind.config.js and add which variants for which property you want to activate on variants:

```js
variants: {
    //[property]: [active variants array]
    backgroundColor: ["responsive", "hover", "focus", "active"],
},
```

- The order matters, the order goes from least to most important.
