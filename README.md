# Guidelines

⭐ If you find these guidelines useful, please star this repo! ⭐

You can suggest changes by creating an issue or a pull request.

This will recap most of the best practices you could have when doing web development. It will
be splitted into several parts.

Of course this is just guidelines, be creative if some parts are missing

1. Git commit messages format
2. Git branches format
3. Code comments
4. Naming conventions
5. ESLint rules
6. File formatting
7. React file structure
8. CI/CD
9. Internal documentation
10. Use a team management tool
11. Use one library that solves a specific problem
12. .vscode folder

## 1. Git commit messages format

Commit messages should respect some certain format. Please provide a clear and concise description about your commit. And don't be afraid to commit a lot.

```txt
[<tag>] (<id?>) - <description>
```

List of different tags possible

```
[FEAT] - The one you will use the most: a new feature, component or function
[FIX] - Bugfix
[CHORE] - Update dependencies, readme or non-changing code files

[REFACTOR] - Code refactoring
[FORMAT] - ESLint or stylistic reformatting
[CLEANUP] - File, directory, library or code removal
[STRUCTURE] - File structure update / migration

[PERF] - Performance improvement
[CONFIG] - Init or configuration files

[TEST] - Unit/integration/e2e tests
[CI/CD] - Continuous Integration / Continuous Deployment

[DOCS] - Internal or external documentation
[A11Y] - Accessibility improvement
[I18N] - Internationalization improvement
[SEO] - Search Engine Optimization

```

### Examples

```txt
[FEAT] Added login & register page
[FIX] Fixed close animation on Modal component
[CHORE] Updated NextJS version

[REFACTOR] Hook for geolocation
[FORMAT] Switched to 2 spaces instead of tabs
[CLEANUP] Removed unused `polished` library
[STRUCTURE] Changed file structure to a more organized one

[PERF] Virtualized list
[CONFIG] Changed `tsconfig` config to set `noUncheckedAccess` to true

[TEST] Unit test on date format functions
[CI/CD] Github actions for deployment & Dockerfile

[DOCS] Dashboard components added in storybook
[A11Y] Improved keyboard navigation
[I18N] Added French language
[SEO] Meta tags updated
```

Some tags are rarely used (such as STRUCTURE) but it is still important to be clear about what your commit changes.
SEO is a bit technical and meta tags are apparently a myth, but it's still there because it's a well-known concept.
Feel free to be creative if none of the above fits!

## 2. Git branches name format

Branches should respect some certain format

- [Naming git branches](https://tilburgsciencehub.com/building-blocks/collaborate-and-share-your-work/use-github/naming-git-branches/)
- [Git branches name convention](https://dev.to/couchcamote/git-branching-name-convention-cch)

Names must be in kebab-case

```txt
main (or master) - The unique source of truth: this branch is used in production
dev - Like main, but for development: it gathers the whole project

features/{name} - Working on a dedicated feature.
features/{ticketId}/{name} - Working on a dedicated feature on the {ticketId} id
bugfix/{name} - Bugfix of {name}
bugfix/{ticketId}/{name} - Bugfix of {name} on the {ticketId} id
hotfix/{name} - Hotfix of {name}
hotfix/{ticketId}/{name} - Hotfix of {name} on the {ticketId} id
migration/{target} - When you have to migrate from a specific lib/language towards another, known as target
docs/{featureName} - Internal or external documentation for a feature
```

### Examples

```txt
main
dev

features/dashboard
features/BELT-10/login-form
bugfix/cart-panel-not-showing
bugfix/BELT-15/wrong-dashboard-routing
hotfix/form-not-submitting
hotfix/BELT-20/support-form-not-submitting
migration/typescript
docs/dashboard
```

## 3. Code comments

Code comments can have a certain format, especially for things you may rework later. Comments must be just above the thing to work on

```txt
// <type> [<?TAG IDENTIFIER>] <description>
```

Here are some comment types you can use: `TODO`, `FIXME`, `WARN`, `DANGER`...
Here are some comment tag identifiers you can use: `A11Y`, `SECURITY`, `I18N`, `PERF`...

This is not necessary to write `<type>` several times when writing a multiline comment. Note this is not strict and you don't really need to add a tag identifier to it, but it can be faster to find if you need to work on some specific things

### Examples

```txt
// TODO add timer feature here
// TODO [A11Y] missing keyboard navigation
// FIXME this is a known and important bug
// FIXME [FORMAT] wrong date format
// WARN might take longer to complete the request

-- multiline example:
// TODO [TYPESCRIPT] this returns some AdminData type but this function
// only provides a UserData type: it requires to know what it returns to
// type it properly
```

To force your coworkers to use these structured code comments, there are two extensions that work well
together, in which you can customize the colors of the comments according to the `<type>` and `[TAG]`.

To include these extensions, you can add into your `.vscode/extensions.json` the following code:

`.vscode/extensions.json`:

```js
{
  "recommendations": [
    "wayou.vscode-todo-highlight",
    "aaron-bond.better-comments"
    // ... your other recommendations
  ]
}
```

And then add some settings to it into the `.vscode/settings.json`
to configure the colors/font styling according to your keywords just like below:

Feel free to customize it for your team.

`.vscode/settings.json`:

```json
{
  "better-comments.tags": [
    {
      "tag": "TODO",
      "color": "#00FFF2",
      "backgroundColor": "#001C1B"
    },
    { "tag": "WARN", "color": "#FF8C00", "backgroundColor": "#1C0F00" },
    { "tag": "FIXME", "color": "#F1411A", "backgroundColor": "#1C0803" },
    {
      "tag": "DANGER [SECURITY]",
      "color": "#e55",
      "bold": true,
      "backgroundColor": "#1C0404"
    },
    { "tag": "DANGER", "color": "#e55", "backgroundColor": "#1C0404" },
    {
      "tag": "INFO",
      "color": "#3498DB",
      "italic": true,
      "backgroundColor": "#07131C"
    },
    { "tag": "//", "color": "#474747", "strikethrough": true }
  ],
  "todohighlight.isEnable": true,
  "todohighlight.isCaseSensitive": true,
  "todohighlight.defaultStyle": {
    "borderRadius": "4px"
  },
  "todohighlight.keywords": [
    { "text": "[TS]", "color": "#A7D3FF", "backgroundColor": "#25415C" },
    { "text": "[REFACTOR]", "color": "#e55", "backgroundColor": "#0000" },
    { "text": "[A11Y]", "color": "#5c5", "backgroundColor": "#0000" }
  ]
}
```

The settings above will produce this render:

![Render of code comments with the extensions mentionned above](/assets/highlighted-code-comments.png)

## 4. Naming convention

To enforce some naming convention, you can use eslint rules for this. See section #5 below for more information. Here are some examples about it

- `null` and `undefined` are different and must be used sparingly. `null` is to set something as "not a thing", **explicitly**. While `undefined` is to set something as "not a thing" **implicitly**

- Typescript interfaces must NOT start with the I prefix we sometimes see. This is a bad practice.
  For components, use the suffix `Props` at the end of your interface. Interfaces must be in PascalCase

```tsx
interface SwitchProps {
  isChecked?: boolean;
  onChange?: () => void;
}

const Switch: React.FC<SwitchProps> = ({ isChecked, onChange }) => {
  return <>...</>;
};

export default Switch;
```

- Booleans must have a verb prefix, such as `is`, `can`, `should`, `has`... just like the `SwitchProps`'s `isChecked` example above. Every truthy boolean value must add a feature and not remove it, even when the default value is true.

❌ This is **incorrect**:

```ts
interface SomeInterface {
  checked?: boolean;
}

interface SomeInterface {
  hasNoAction?: boolean;
}

interface SomeInterface {
  isNotExpandable?: boolean;
}
```

✅ This is **correct**:

```ts
interface SomeInterface {
  isChecked?: boolean;
}

interface SomeInterface {
  hasAction?: boolean;
}

interface SomeInterface {
  isExpandable?: boolean;
}
```

- Don't use numbers to create a variation of a component. `Header.tsx` is fine, but `Header2.tsx` isn't. Consider either
  changing `Header2` name to a more appropriate one, or merge it into the `Header` as one component if it's similar

❌ This is **incorrect**:

```tsx
const Header = () => {
  return <div>...</div>;
};

const Header2 = () => {
  return <div>...</div>;
};
```

✅ This is **correct**:

```tsx
const Header = () => {
  return <div>...</div>;
};

const DashboardHeader = () => {
  return <div>...</div>;
};
```

- If you have multiple generics, all of them must start with T and each one must be provided a context to it. Example: `TObj` or `TKey`. Use PascalCase after the T prefix. There is no need to have underscores as a prefix or suffix. `TObj_` is incorrect

❌ This is **incorrect**:

```ts
type SomeType<T extends Record<PropertyKey, unknown>, K extends keyof T> = ...
type SomeType<TObj_ extends Record<PropertyKey, unknown>, _TKey extends keyof T> = ...
```

✅ This is **correct**:

```ts
type SomeType<TObj, TKey extends keyof TObj> = ...

type LiteralUnion<T extends string> = T | (string & {})

// Even better
type LiteralUnion<TLiteral extends string> = TLiteral | (string & {})
```

- Typescript union type's name should not be plural form. An array should.

❌ This is **incorrect**:

```ts
type Colors = "red" | "blue";

// Don't do that, please
type ColorsArray = Colors[];
```

✅ This is **correct**:

```ts
type Color = "red" | "blue";

type Colors = Color[];
```

Why this? When you type an argument as `Color` in that case, you will be able to provide only one element. It's kind of like an enum, but in less buggy ;)

On top of all of that, a good approach too is to add local snippets (create a .vscode or .idea folder). It will help your team to be more consistent by using your conventions, without much effort

## 5. ESLint rules

[ESLint](https://eslint.org/) helps with finding bugs, reinforce code conventions and helps you to write better code in general by preventing you using deprecated APIs.

ESLint rules all must be set to "error". Warn is an anti-pattern.

The stricter the rules are, the better. Why? Errors encourages you to fix it since it may cause unpredictable bugs or mistakes. Errors don't pass in CI/CD since it exits with a code of 1. Warn exits with 0, which means success in bash. [See exit codes in POSIX](https://shapeshed.com/unix-exit-codes/#:~:text=On%20POSIX%20systems%20the%20standard%20exit%20code%20is%200%20for%20success%20and%20any%20number%20from%201%20to%20255%20for%20anything%20else)

ESLint shouldn't be used for stylistic formatting. Use Prettier instead for that.

[Here you can get my ESLint custom config with typescript or even react](https://www.npmjs.com/package/eslint-config-eskiu), it includes all the naming conventions i quoted above and more

## 6. File formatting

Please, write a `prettier.config.js` file or something similar. This is a complement to ESLint: it will make code style consistent throughout different people. Tell your team to use a formatter.

My personal preference is to use 2 spaces instead of tabs, because some syntax highlighters are making tab width as 8 characters long, which causes excessive indentation and is less readable as a consequence. Spaces are better for this case as well.

Add in your `prettier.config.js` file:

```js
/** @type {import("prettier").Config} */
module.exports = {
  useTabs: false,
  tabWidth: 2,
  semi: true,
  singleQuote: false,

  // You can change the value below but set at least one: `avoid` or `always`
  arrowParens: "avoid", // i choose `avoid` to reduce useless noise

  // If you're using tailwind / tailwind-variants / clsx / cva
  plugins: ["prettier-plugin-tailwindcss"],
  tailwindFunctions: ["tv", "clsx", "cn", "cva", "twMerge"],
};
```

## 7. File structure

From my experience, working with React in mid-sized or big project gets really messy pretty fast.

- IMPORTANT: Don't group your functions in a single file **whose name is too global**, e.g a `request.ts` or `validation.ts` is a bad idea. Use a folder instead in these situations: `/requests/users.ts`, `/validations/auth.ts` where each of those files may contain several functions, like `loginSchema()` or `signupSchema` in the `auth.ts` file. No, a `types` file is probably not enough and may contain too many types of different contexts. Be creative, organized and meaningful
- [Don't put your types here by Matt Pocock](https://www.youtube.com/watch?v=zu-EgnbmcLY)
- [Junior vs Senior React Folder Structure - How To Organize React Projects](https://youtu.be/UUga4-z7b6s?si=d4ahpgcavZe1Zjc6&t=581)
- Zustand stores and React contexts are used for different reasons. Stores are used as shared data across the entire project/feature, while contexts can be provided different data thanks to the Provider component and the value prop. If you are going to use [the compound pattern](https://www.patterns.dev/posts/compound-pattern), you can use React's context and put it directly in the component file itself instead of putting it in a /contexts directory. Don't use stores for that case, only for global state.

Here is a useful file structure for real projects. It can vary according to different libraries usage

```bash
/src                 # Source directory
  /assets            # Images, fonts, logos, GIFs, videos, SVGs...
  /components        # Global components
  /data              # Static data, constants
  /features          #
    /{featureName}   #
      /components    # Components related to {featureName}
      /hooks         # Custom hooks related to {featureName}
      /utils         # Utils functions related to {featureName}
      /stores        # Global stores. Could be named `context`, but if you're using it in the whole app, it may cause performance issue. Name it `stores` if you're using zustand
  /hooks             # Global custom hooks
  /layouts           # Global layouts: Footer, Navbar (...)
  /lib               # Façade pattern, for example you can instanciate axios in a file here, or react-query queryKeys/queryFns
  /pages             # Pages
  /stores            # Global stores. Could be named `context`, but if you're using it in the whole app, it may cause performance issue. Name it `stores` if you're using zustand, or whatever name your global state library uses
  /stories           # If using storybook, internal documentation
  /utils             # Util functions: date format, price format...

  .dockerignore      # Docker ignore file
  .env               # Your env variables
  .env.example       # Use this as a template so the other people can copy it: it has dummy values .env.example should appear in the git repo
  eslint.cjs         # ESLint configuration
  .gitignore         # Git ignore
  prettier.config.js # Prettier configuration
  Dockerfile         # Dockerfile
  global.d.ts        # Global types
  package.json       # package.json: Scripts, libraries used.
  README.md          # README: global information about the project, how to run it, where to find documentation, how the team is organized
  reset.d.ts         # Typescript reset if you are using @total-typescript/ts-reset
  tsconfig.json      # TS config
  ...                # Other configuration files, test config...
```

package.json may have at least these scripts:

```js
{
  "scripts": {
    "start": "...", // Start the app in production mode
    "dev": "...", // Start the app in dev mode
    "build": "...", // Build the app for production
    "docs": "...", // If using storybook or similar docs technology
    "lint": "...", // Lint the files
    "tscheck": "...", // Check silently typescript types
    "format": "...", // Format the file
    "test:unit": "...", // Unit tests
    "test:e2e": "...", // End-to-end tests

    // You can also have some scripts for database migrations
    "db:migrate": "...",
    "db:studio": "...",
    "db:push": "...",
  }
}
```

## 8. CI/CD

CI/CD will help you automate things like deployment for instance. There are a lot of CI/CD tools, but I'm not an expert in this field so i can't really recommend you one or another, Github Actions is very popular and is straight-forward

## 9. Internal documentation

Write at least clear internal documentation. This will be helpful for new developers, but also for you if you come back into it a few months later,
just in case you forget

Storybook is an ok tool to do that, you basically write your documentation through `.mdx` files and you can also preview your React components
by isolating them

## 10. Use a team management tool

Jira is quite opinionated, but still has great features and has a lot of different plugins to integrate with other SaaS

## 11. Use one library that solves a specific problem

Well, this one is kind of obvious, but basically find what problems you meet, and then you can implement a library to solve it. And ALL THE TEAM should use it. How many times i've seen projects using different solutions for the same problem. Imagine seeing tailwind, MUI, styled-components, emotion, scss, stylus used in the same project. How silly.

### Examples

Note those examples are my personal favorites. There are plenty of other alternatives, but by experience i can tell those are the most popular and performant libs. See below the reasons of these choices

Note 2: Don't use tailwind with a UI library/framework that uses another styling system like MUI (that has built-in accessibility and uses emotion). If you want to use tailwind, you may want to use a tailwind-based component library as listed in the example, or an unstyled one that provides you built-in accessibility so you don't have to waste extra time on it

```bash

- Styling: Tailwind
- Accessibility: any UI framework: HeadlessUI, NextUI, shadcnUI... # Most of them have built-in a11y support so you don't have to write it by yourself
- Handling variants: tailwind-variants # or cva (class-variance-authority)
- Conditional classes: clsx # or cn

- Animations: framer-motion

- Form handling: react-hook-form
- Schema validation: zod # or valibot

- Global state manager: valtio, xState, zustand
- Requests: react-query

- Date manipulation: dayjs # or date-fns

- Internal documentation: Storybook
- ...

```

#### Why Tailwind?

Tailwind seems to be silly at first, but is actually very smart. The usage with PostCSS is good because it will remove the unused class across the entire project. Tailwind works well in any framework too, even in rust-based fullstack frameworks like Leptos. Moreover, imagine using some preprocessor like sass.

Using sass will:

- require energy to find a good class name for nothing
- duplicate a lot of common used properties like `display: flex;`: that's 14 characters! Plus the class name selector

Using Tailwind instead of sass will:

- use only one small class name for a specific task, like the `display: flex;` example above
- not require energy since the class names are intuitive
- "force" you to use their good conventions, like palettes and spacing systems

#### Why react-hook-form over formik?

Formik rerenders the whole form on every keystroke. react-hook-form will not, thus it is more performant in rendering process. It has the same good features as well and is faster overall

#### What is tailwind-variants and CVA?

[CVA](https://cva.style/docs) is a wonderful util library that helps you writing easily variants, colors, shapes, and mix them depending on props.

[Tailwind-variants](https://www.tailwind-variants.org/docs/introduction) is highly inspired by CVA (see above) and has extra interesting features, like extending from a base variant, applying variants according to the viewport width and so on

#### Zod? Valibot?

[Zod](https://zod.dev/) is the go-to choice for schema validation. It can be used anywhere: server-side, client-side, in forms or to be sure you have correct ENV variables during **runtime**. This is strongly typed, and can be a bit compared to typescript but during runtime, while having more features like `refine` and other good stuff such as explicit optional values. By default, all the values are required, which is stricter but also better. This is why i went from using `yup` to `zod` at first. We'll see later that there is a lighter alternative, but its API is built differently.

Basically, everything that can be modified by the user or an external source should be verified **during runtime**. It shouldn't cost much performance.

You MUST be obsessed with validation.

Use data validation for different scenarios:

- API responses. Validate them, your app is mostly based on those. tRPC mixed with typesafe ORMs/ODMs must be enough since your database schema is linked to your favorite ORM/ODM, thanks to codegen (Prisma) or pure TypeScript (Drizzle, Mongoose, typeORM, Sequelize...), else please verify your API responses from the database to the backend (if you don't use any ORM/ODM), and from the backend to the frontend if your fullstack is not linked. It will also help you showing custom error messages if the verification fails.
- 3rd-party API responses, in frontend AND in backend (This can lead to unexpected rendering if the API changes its shape)
- URL query params. Yes in fact, if you have some sort of enum or restricted values, using zod is a very good typesafe runtime solution for this. Anyone can change the URL with an unexpected param. DON'T trust your users. Your app should be smooth to the user. Applies to frontend and backend too
- localStorage, sessionStorage (...). You can't know if the user will change or not the values stored in his browser.
- Form data. Do data validation for frontend **AND** backend for this for obvious reason. Frontend validation is more likely to give feedback to the user, for example the email shape is wrong and you have to show an error, instead of waiting the server response. It also integrates well with `react-hook-form`
- Webhooks. Same reason, you can't trust the response schema.
- .env variables. [There is a package **for NextJS** made by the @t3-oss foundation that makes it very easy to use](https://github.com/t3-oss/t3-env) that i recommend if you are using NextJS, although a simple `env.ts` file at the root of the repo is usually enough. If you want to type your `process.env` properly according to the schema, you can with the utility type `z.infer<typeof envSchema>` and extending [the `ProcessEnv` interface](https://stackoverflow.com/questions/45194598/using-process-env-in-typescript), see my code below

env.ts:

```ts
import { z } from "zod";

// Force the schema to have uppercase keys and string or a string enum zod constructor for each value
type EnvObj = Record<
  Uppercase<string>,
  z.ZodString | z.ZodEnum<[string, ...string[]]>
>;

const envSchema = z.object({
  EPIC: z.string().url(),
  WOW: z.string().min(3),
  MAGICS: z.string(),
  TYPESCRIPT_WIZARD: z.enum(["wizardry", "ts", "next"]),
} satisfies EnvObj);

export type EnvSchema = z.infer<typeof envSchema>;

const env = envSchema.parse({
  EPIC: process.env.EPIC,
  // this "WOW" env will error during runtime: it does not include at least 3 characters according to the schema
  WOW: "",
  MAGICS: process.env.MAGICS,
  TYPESCRIPT_WIZARD: process.env.TYPESCRIPT_WIZARD, // $ExpectType: "wizardry" | "ts" | "next"
} satisfies EnvSchema);

export default env;
```

global.d.ts:

```ts
import type { EnvSchema } from "@/env";

declare global {
  namespace NodeJS {
    // Your process.env has now autocomplete according to your zod schema!
    interface ProcessEnv extends EnvSchema {}
  }
}

export {};
```

Now that you see why validation is important and how to use it in a lot of places, [i'll talk about `Valibot`](https://valibot.dev/). This zod alternative is based on imports, thus it is way lighter. Zod returns objects with methods that you can't treeshake, and the goal of a SSR-based framework like NextJS is to reduce client-side javascript on hydration thanks to RSCs. Valibot is a very interesting library in this case, most of the time for client-side validation (dynamic URL search params & forms for example) you don't need extra complicated features that zod offers, you just need to validate basic shapes, usually. And Valibot is perfect for that. Plus, react-hook-form gives us a resolver for Valibot, which makes it even better. Note: you can still use zod in the server side because the server has already downloaded zod and doesn't need to anymore. Note that having Valibot and Zod in the same project will not allow you to share a schema between your frontend and backend, because Valibot is not a zod extension. You can still use zod in the backend and Valibot in the frontend, but you will have to write two different schemas. This is not a big deal, but it's still a thing to consider.

- [When to use Zod? Don't use compile-time-only checking!](https://www.youtube.com/watch?v=AeQ3f4zmSMs)
- [Valibot documentation](https://valibot.dev/)
- [Valibot: Functions imports make bundle size much lighter](https://www.builder.io/blog/valibot-bundle-size)

#### Date manipulation: Dayjs is the best tradeoff

In fact, dayjs is very lightweight compared to date-fns, and will be more than enough for most projects. Its API is also rich and has useful features, it is typesafe too. Date-fns has even more features, but it seems quite overkill for client-side most of the time

## 12. `.vscode` folder

`.vscode` folder (and .idea equivalent for Jetbrains users), is an underestimated feature of your favorite IDE. In fact, you can
share settings, snippets, extensions recommendations and more. It is located at the root of your project.

### `.vscode/settings.json`

In order to enforce some rules, you can add some settings to your `settings.json` file. This file is specific to your project. It will override the global settings of your team members. Some settings are essential, like the location of your typescript SDK (version).

I will list useful settings of different extensions to increase consistency in your team. You shouldn't neglect this point,
it will save you time and energy.

#### Settings for typescript

The story: i was working on a project at my internship when i realized my TS version in VSCode was 5.3-dev, while the
typescript version in the project was 5.2.2 or something. There are improved things in the 5.3 version, and i was using them.
Basically, in the 5.3 version, you can remove the `readonly` modifier when doing `... as const satisfies readonly unknown[]`.
I removed the `readonly` modifier because it's not necessary anymore, but it was causing typescript errors in the project
for people that were using the 5.2 version. Later, i was looking at tailwind-variants' github and found in their `settings.json`
that they were setting `typescript.tsdk: "node_modules/typescript/lib"` in it, which would have avoid my
problem. I was using a different typescript version instead, which was not the same as the project's one.

Also, one of my coworker was changing the import path manually, while it can be done automatically.
A time-saver option is to update imports automatically when a file is moved, a good example is when you move a component
to a different folder for some reason. It will update the import path automatically. and you won't have to worry about that

You can now add this to your `.vscode/settings.json` file:

```json
{
  "typescript.tsdk": "node_modules/typescript/lib",
  "typescript.enablePromptUseWorkspaceTsdk": true,
  "javascript.updateImportsOnFileMove.enabled": "always",
  "typescript.updateImportsOnFileMove.enabled": "always"
}
```

#### Settings for formatting & linting

You may think formatting on save is just preference, but you are probably wrong. It will enforce your team to format the files
before pushing them.

What will happen if one member pushes without formatting ? When someone with the formatter on save will pull the code, it will
reformat the file, and you will potentially have merge conflicts. Format on save is a must-have. And also a fix all lints on save

To enable this recommendation, you can add to your `.vscode/settings.json`:

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true
}
```

#### Settings for tailwind / cva / tailwind-variants

If you are using tailwind, you may want to have autocomplete for the classes, even in your favorite variants library like
tailwind-variants.

Assuming you already have eslint and prettier configs, you can add this to your `.vscode/settings.json`:

```json
{
  "tailwindCSS.classAttributes": ["class", "className", "ngClass"],
  "tailwindCSS.experimental.classRegex": [
    ["cva\\(([^)]*)\\)", "[\"'`]([^\"'`]*).*?[\"'`]"],
    ["cx\\(([^)]*)\\)", "(?:'|\"|`)([^']*)(?:'|\"|`)"],
    ["tv\\(([^)]*)\\)", "[\"'`]([^\"'`]*).*?[\"'`]"]
  ]
}
```

#### Settings for Prisma

When working with Prisma, you will probably need autocomplete for Prisma, and the prisma formatter.

You can add to your `.vscode/settings.json`:

```json
{
  "[prisma]": {
    "editor.defaultFormatter": "Prisma.prisma"
  }
}
```

### `.vscode/extensions.json`

In order to recommend some good extensions for your workflow, you can add some extensions to your `extensions.json` file. This file is specific to your project.

These extensions are the one i consider very good for team members:

```js
{
  "recommendations": [
    // Essentials
    "dbaeumer.vscode-eslint",        // ESLint
    "esbenp.prettier-vscode",        // Prettier
    "aaron-bond.better-comments",    // Better comments
    "wayou.vscode-todo-highlight",   // Highlight, see section #3
    "usernamehw.errorlens",          // Error Lens: display the errors to the screen directly
    "wix.vscode-import-cost",        // Import cost: size of the imported variables
    "eamodio.gitlens",               // Git history, blame, ...
    "yoavbls.pretty-ts-errors",      // Better TS errors explanations

    // If using tailwind
    "tailwindlabs.tailwindcss-intellisense", // Show the classes and colors in the autocomplete

    // Can improve your productivity
    "formulahendry.auto-close-tag",         // Close HTML tags automatically
    "formulahendry.auto-rename-tag",        // Rename HTML tags automatically
    "meganrogge.template-string-converter", // Convert "" to `` when typing ${

    // If using prisma
    "prisma.prisma", // Prisma LSP (syntax highlighting, autocomplete & autofix)
  ]
}
```

## IDEAS

- Add A/B testing if needed
- Telemetry
- [Conventionnal commits](https://www.conventionalcommits.org/en/v1.0.0/#summary)
- [MUST, MAY, SHOULD...](https://www.ietf.org/rfc/rfc2119.txt)
- Add `.vscode/snippets.code-snippets` file to share snippets with your team
- For advanced TS wizards, you can check hotscript & type-fest

- good things to do:
  - testing if you don't have anything more to do. Prefer end-to-end testing first, because it will be closer to user actions than unit testing
  - in react prefer React.ReactNode over string when it's for displaying things only (number doesn't have the same methods as string so it will error if string is the type). Do this because sometimes you may need a component instead
  - props spreading must be done right after the component name / HTML element name (`<Component {...props} yourProps={}></Component>`) so it doesn't overrides your props. Anyway, shouldn't happen if you use `Omit<T>`
  - Use `React.ComponentPropsWithoutRef<"div">` instead of `React.HTMLProps<HTMLDivElement>`. Precise if the targetted element has a ref or not. More explaination in the github link below Sources:
    - https://stackoverflow.com/questions/48198180/what-is-the-difference-between-react-htmlprops-and-react-htmlattributest
    - https://github.com/typescript-cheatsheets/react/blob/main/docs/advanced/patterns_by_usecase.md#componentprops

## Note

This was inspired by many articles and videos

- [How to write better git commit messages](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/)
- [Naming git branches](https://tilburgsciencehub.com/building-blocks/collaborate-and-share-your-work/use-github/naming-git-branches/)
- [Git branches name convention](https://dev.to/couchcamote/git-branching-name-convention-cch)
- [Junior vs Senior React Folder Structure - How To Organize React Projects](https://youtu.be/UUga4-z7b6s?si=d4ahpgcavZe1Zjc6&t=581)
- [Don't put your types here by Matt Pocock](https://www.youtube.com/watch?v=zu-EgnbmcLY)
- [When to use Zod? Don't use compile-time-only checking!](https://www.youtube.com/watch?v=AeQ3f4zmSMs)
- [Difference between React.HTMLProps and React.HTMLAttributes](https://stackoverflow.com/questions/48198180/what-is-the-difference-between-react-htmlprops-and-react-htmlattributest)
- [React.ComponentProps best practices](https://github.com/typescript-cheatsheets/react/blob/main/docs/advanced/patterns_by_usecase.md#componentprops)

I know this does not fit in all the extra edge cases, but it's still better than an unorganized team

If you found it useful, don't forget to star it! ⭐

## Interesting articles

- [Useful types with type-fest](https://www.xpbytes.com/articles/types-you-should-know-about-typescript/)
- [Compose your types with hotscript](https://github.com/gvergnaud/hotscript)
- [Advanced React typescript patterns](https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase/)

## TODO

- I should move the different topics into different markdown files, this readme gets longer and longer
- talk about [husky](https://typicode.github.io/husky/) to run scripts before anyone commits
- talk about [separation of concerns](https://youtu.be/eMTFzpxR0QQ?si=188gvdCGWPv37PJ7)
- talk about [SOLID principle with advanced examples](https://youtu.be/t_h_A6RkM7A?si=VDLS3Ts7DLr3UQwi) (i knew about SOLID before, but this video is very good)
