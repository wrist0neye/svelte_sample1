# sv

Everything you need to build a Svelte project, powered by [`sv`](https://github.com/sveltejs/cli).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npx sv create

# create a new project in my-app
npx sv create my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.


### ChangeLog
#### 2024-12-16 Mon
- `sketch_book` div component moves from *ResizableTable.svelte* to *+page.svelte*
- add `resize add_col/row/table` button.

> I need to restart ResizableTable code. I shouldn't use `onMount()` code on Resizable Code because webpage will be restart when I add / remove ResizableTable everytime.

- [ ] double click event
    - [ ] edit titlemenu
    - [ ] add text div (clicked on sketchbook)
- [ ] click event
    - [ ] edit `td>div` components
- [ ] table `sticky`
    - [ ] https://velog.io/@planic324/%ED%8B%80%EA%B3%A0%EC%A0%95-%ED%85%8C%EC%9D%B4%EB%B8%94%EC%9D%84-%EB%A7%8C%EB%93%A4%EC%96%B4%EB%B3%B4%EC%9E%90
- [ ] remove `onMount()` in *ResizableTable*.
- [ ] right click
- [ ] `ctrl` + `mousemove`/`mouseup`
    - [ ] copy table
    - [ ] resize button
- [ ] `shift` + `mousemove`/`mouseup`
    - [ ] move orthogonal
- [ ] `drag` tooltip