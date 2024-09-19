# NEXT DASHBOARD APP
## guide link
[next learn](https://nextjs.org/learn/dashboard-app/css-styling)

## setup
```bash
npm install -g pnpm
npx create-next-app@latest nextjs-dashboard --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example" --use-pnpm```
cd nextjs-dashboard
```

/app: Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.
/app/lib: Contains functions used in your application, such as reusable utility functions and data fetching functions.
/app/ui: Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.
/public: Contains all the static assets for your application, such as images.

Config Files: You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.

```bash
pnpm i
pnpm dev
```

[Mockup api](https://mockapi.io/projects/66eaca7e55ad32cda47a6a79)

[Prisma](https://www.prisma.io/) automatically generates types based on your database schema.

------------

## css
CSS Modules Provide a way to make CSS classes locally scoped to components by default, reducing the risk of styling conflicts.

file: /app/ui/home.module.css

```css
.shape {
  height: 0;
  width: 0;
  border-bottom: 30px solid black;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```
file: /app/page.tsx

`import styles from '@/app/ui/home.module.css';`

`<div className={styles.shape} />`


## fonts

file: /app/ui/fonts.ts
```ts
import { Inter } from 'next/font/google';
export const inter = Inter({ subsets: ['latin'] });
```
file: /app/layout.tsx

`import { inter } from '@/app/ui/fonts';`

`<body className={`${inter.className} antialiased`}>{children}</body>`


## images
The <Image> Component is an extension of the HTML <img> tag, and comes with automatic image optimization, such as:

Preventing layout shift.
Resizing images.
Lazy loading by default.
Serving images in modern formats.


----------

# QUESTIONS

1. ## diff btwn `<div className={styles.shape}></div>` and `<div className={styles.shape} />`.

`<div className={styles.shape}></div>`: Use this when you have child elements or text.

`<div className={styles.shape} />`: Use this for an empty <div> with no children.


2. ## `<div className="relative w-0 h-0 border-l-[15px] border-r-[15px] border-b-[26px] border-l-transparent border-r-transparent border-b-black"/>` why would i write this instead of css where i can write less code?

Using Tailwind in JSX provides **faster development**, **consistent design**, and **dynamic styling** without switching to CSS files. However, it makes JSX more **verbose** and harder to maintain compared to using separate, **reusable CSS classes** that keep your code cleaner. Tailwind is best for quick, small projects, while CSS is better for larger, more complex ones.


# QUESTIONS/typescript

1. ## `function InvoiceStatus({ status }: { status: string })` vs `function InvoiceStatus({ status: newStatus }: { status: string })`

First one uses **destructuring** to extract the `status` property from an object argument and **type annotation** to specify that `status` is of type `string`.
Second does an additional task of renaming the status parameter to newStatus.


2. ## using type vs Interface for Object Shape

Use **type** when you need union types, intersection types, or more complex type manipulations.
```ts
type Person = { name: string; age: number; };
let person: Person = { name: "Alice", age: 30 };
type Status = "active" | "inactive"; // Union type
type PersonWithAddress = Person & Address; // Intersection type
```
Use interface when you need to define a clear object shape that might be extended or merged, especially if you expect your types to be part of a public API or library.
```ts
interface Person { name: string; age: number; }
let person: Person = { name: "Alice", age: 30 };
interface Employee extends Person { employeeId: number; }
let employee: Employee = { name: "Bob", age: 25, employeeId: 1234 };
```

3. ## using generics in types 

Defines a generic type Response<T> where data can be of any type T
```ts
type Response<T> = { status: number; data: T; };
let stringResponse1: Response<string> = { status: 200, data: "Success" };
let numberResponse: Response<number> = { status: 200, data: 1 };
```

4. ## does having both a generic and a non-generic type with the same name in TypeScript cause a naming conflict?

AdminUser is a non-generic type combining User, Admin, and an additional lastLogin property.
```ts
type AdminUser = User & Admin & {lastLogin: Date; };
let adminUser1: AdminUser = {
  name: "Alice",
  adminRights: ["manage_users", "view_reports"],
  lastLogin: new Date()
};
```
AdminUser<T> is a generic type allowing any additional properties via T. adminUser uses this generic type to include a lastLogin property alongside User and Admin properties.
```ts
type AdminUser<T> = User & Admin & T;
let adminUser2: AdminUser<{ lastLogin: Date }> = {
  name: "Bob",
  adminRights: ["manage_users"],
  lastLogin: new Date()
};```

