---
title: Creating an item component
slug: Learn_web_development/Core/Frameworks_libraries/Angular_item_component
page-type: learn-module-chapter
sidebar: learnsidebar
---

{{PreviousMenuNext("Learn_web_development/Core/Frameworks_libraries/Angular_styling","Learn_web_development/Core/Frameworks_libraries/Angular_filtering", "Learn_web_development/Core/Frameworks_libraries")}}

Components provide a way for you to organize your application. This article walks you through creating a component to handle the individual items in the list, and adding check, edit, and delete functionality. The Angular event model is covered here.

<table>
  <tbody>
    <tr>
      <th scope="row">Prerequisites:</th>
      <td>
        Familiarity with the core <a href="/en-US/docs/Learn_web_development/Core/Structuring_content">HTML</a>,
        <a href="/en-US/docs/Learn_web_development/Core/Styling_basics">CSS</a>, and
        <a href="/en-US/docs/Learn_web_development/Core/Scripting">JavaScript</a> languages,
        knowledge of the
        <a
          href="/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line"
          >terminal/command line</a
        >.
      </td>
    </tr>
    <tr>
      <th scope="row">Objective:</th>
      <td>
        To learn more about components, including how events work to handle
        updates. To add check, edit, and delete functionality.
      </td>
    </tr>
  </tbody>
</table>

## Creating the new component

At the command line, create a component named `item` with the following CLI command:

```bash
ng generate component item
```

The `ng generate component` command creates a component and folder with the name you specify.
Here, the folder and component name is `item`.
You can find the `item` directory within the `app` folder:

```plain
src/app/item
├── item.component.css
├── item.component.html
├── item.component.spec.ts
└── item.component.ts
```

Just as with the `AppComponent`, the `ItemComponent` is made up of the following files:

- `item.component.html` for HTML
- `item.component.ts` for logic
- `item.component.css` for styles
- `item.component.spec.ts` for testing the component

You can see a reference to the HTML and CSS files in the `@Component()` decorator metadata in `item.component.ts`.

```ts
@Component({
  selector: "app-item",
  standalone: true,
  imports: [],
  templateUrl: "./item.component.html",
  styleUrl: "./item.component.css",
})
export class ItemComponent {
  // …
}
```

## Add HTML for the ItemComponent

The `ItemComponent` can take over the task of giving the user a way to check items off as done, edit them, or delete them.

Add markup for managing items by replacing the placeholder content in `item.component.html` with the following:

```html
<div class="item">
  <input
    [id]="item.description"
    type="checkbox"
    (change)="item.done = !item.done"
    [checked]="item.done" />
  <label [for]="item.description">\{{item.description}}</label>

  @if (!editable) {
  <div class="btn-wrapper">
    <button class="btn" (click)="editable = !editable">Edit</button>
    <button class="btn btn-warn" (click)="remove.emit()">Delete</button>
  </div>
  }

  <!-- This section shows only if user clicks Edit button -->
  @if (editable) {
  <div>
    <input
      class="sm-text-input"
      placeholder="edit item"
      [value]="item.description"
      #editedItem
      (keyup.enter)="saveItem(editedItem.value)" />

    <div class="btn-wrapper">
      <button class="btn" (click)="editable = !editable">Cancel</button>
      <button class="btn btn-save" (click)="saveItem(editedItem.value)">
        Save
      </button>
    </div>
  </div>
  }
</div>
```

The first input is a checkbox so users can check off items when an item is complete.
The double curly braces, `\{{}}`, in the `<label>` for the checkbox signifies Angular's interpolation.
Angular uses `\{{item.description}}` to retrieve the description of the current `item` from the `items` array.
The next section explains how components share data in detail.

The next two buttons for editing and deleting the current item are within a `<div>`.
On this `<div>` is an `@if` block that you can use to render parts of a template based on a condition.
This `@if` means that if `editable` is `false`, this `<div>` is rendered in the template. If `editable` is `true`, Angular removes this `<div>` from the DOM.

```html
@if (!editable) {
<div class="btn-wrapper">
  <button class="btn" (click)="editable = !editable">Edit</button>
  <button class="btn btn-warn" (click)="remove.emit()">Delete</button>
</div>
}
```

When a user clicks the **Edit** button, `editable` becomes true, which removes this `<div>` and its children from the DOM.
If, instead of clicking **Edit**, a user clicks **Delete**, the `ItemComponent` raises an event that notifies the `AppComponent` of the deletion.

An `@if` is also on the next `<div>`, but is set to an `editable` value of `true`.
In this case, if `editable` is `true`, Angular puts the `<div>` and its child `<input>` and `<button>` elements in the DOM.

```html
<!-- This section shows only if user clicks Edit button -->
@if (editable) {
<div>
  <input
    class="sm-text-input"
    placeholder="edit item"
    [value]="item.description"
    #editedItem
    (keyup.enter)="saveItem(editedItem.value)" />

  <div class="btn-wrapper">
    <button class="btn" (click)="editable = !editable">Cancel</button>
    <button class="btn btn-save" (click)="saveItem(editedItem.value)">
      Save
    </button>
  </div>
</div>
}
```

With `[value]="item.description"`, the value of the `<input>` is bound to the `description` of the current item.
This binding makes the item's `description` the value of the `<input>`.
So if the `description` is `eat`, the `description` is already in the `<input>`.
This way, when the user edits the item, the value of the `<input>` is already `eat`.

The template variable, `#editedItem`, on the `<input>` means that Angular stores whatever a user types in this `<input>` in a variable called `editedItem`.
The `keyup` event calls the `saveItem()` method and passes in the `editedItem` value if the user chooses to press enter instead of click **Save**.

When a user clicks the **Cancel** button, `editable` toggles to `false`, which removes the input and buttons for editing from the DOM.
When `editable` is `false`, Angular puts `<div>` with the **Edit** and **Delete** buttons back in the DOM.

Clicking the **Save** button calls the `saveItem()` method.
The `saveItem()` method takes the value from the `#editedItem` element and changes the item's `description` to `editedItem.value` string.

## Prepare the AppComponent

In the next section, you will add code that relies on communication between the `AppComponent` and the `ItemComponent`.
Add the following line near the top of the `app.component.ts` file to import the `Item`:

```ts
import { Item } from "./item";
import { ItemComponent } from "./item/item.component";
```

Then, configure the AppComponent by adding the following to the same file's class:

```ts
export class AppComponent {
  // …
  remove(item: Item) {
    this.allItems.splice(this.allItems.indexOf(item), 1);
  }
  // …
}
```

The `remove()` method uses the JavaScript `Array.splice()` method to remove one item at the `indexOf` the relevant item.
In plain English, this means that the `splice()` method removes the item from the array.
For more information on the `splice()` method, see the [`Array.prototype.splice()` documentation](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice).

## Add logic to ItemComponent

To use the `ItemComponent` UI, you must add logic to the component such as functions, and ways for data to go in and out.
In `item.component.ts`, edit the JavaScript imports as follows:

```ts
import { Component, Input, Output, EventEmitter } from "@angular/core";
import { CommonModule } from "@angular/common";
import { Item } from "../item";
```

The addition of `Input`, `Output`, and `EventEmitter` allows `ItemComponent` to share data with `AppComponent`.
By importing `Item`, the `ItemComponent` can understand what an `item` is.
You can update the `@Component` to use [`CommonModule`](https://angular.dev/api/common/CommonModule) in `app/item/item.component.ts` so that we can use the `@if` blocks:

```ts
@Component({
  selector: "app-item",
  standalone: true,
  imports: [CommonModule],
  templateUrl: "./item.component.html",
  styleUrl: "./item.component.css",
})
export class ItemComponent {
  // …
}
```

Further down `item.component.ts`, replace the generated `ItemComponent` class with the following:

```ts
export class ItemComponent {
  editable = false;

  @Input() item!: Item;
  @Output() remove = new EventEmitter<Item>();

  saveItem(description: string) {
    if (!description) return;

    this.editable = false;
    this.item.description = description;
  }
}
```

The `editable` property helps toggle a section of the template where a user can edit an item.
`editable` is the same property in the HTML as in the `@if` statement, `@if(editable)`.
When you use a property in the template, you must also declare it in the class.

`@Input()`, `@Output()`, and `EventEmitter` facilitate communication between your two components.
An `@Input()` serves as a doorway for data to come into the component, and an `@Output()` acts as a doorway for data to go out of the component.
An `@Output()` has to be of type `EventEmitter`, so that a component can raise an event when there's data ready to share with another component.

> [!NOTE]
> The `!` in the class's property declaration is called a [definite assignment assertion](https://www.typescriptlang.org/docs/handbook/2/classes.html#--strictpropertyinitialization). This operator tells TypeScript that the `item` field is always initialized and not `undefined`, even when TypeScript cannot tell from the constructor's definition. If this operator is not included in your code and you have strict TypeScript compilation settings, the app will fail to compile.

Use `@Input()` to specify that the value of a property can come from outside of the component.
Use `@Output()` in conjunction with `EventEmitter` to specify that the value of a property can leave the component so that another component can receive that data.

The `saveItem()` method takes as an argument a `description` of type `string`.
The `description` is the text that the user enters into the HTML `<input>` when editing an item in the list.
This `description` is the same string from the `<input>` with the `#editedItem` template variable.

If the user doesn't enter a value but clicks **Save**, `saveItem()` returns nothing and does not update the `description`.
If you didn't have this `if` statement, the user could click **Save** with nothing in the HTML `<input>`, and the `description` would become an empty string.

If a user enters text and clicks save, `saveItem()` sets `editable` to false, which causes the `@if` in the template to remove the edit feature and render the **Edit** and **Delete** buttons again.

Though the application should compile at this point, you need to use the `ItemComponent` in `AppComponent` so you can see the new features in the browser.

## Use the ItemComponent in the AppComponent

Including one component within another in the context of a parent-child relationship gives you the flexibility of using components wherever you need them.

The `AppComponent` serves as a shell for the application where you can include other components.

To use the `ItemComponent` in `AppComponent`, put the `ItemComponent` selector in the `AppComponent` template.
Angular specifies the selector of a component in the metadata of the `@Component()` decorator.
In this example, we've defined the selector as `app-item`:

```ts
@Component({
  selector: "app-item",
  // …
})
export class ItemComponent {
  // …
}
```

To use the `ItemComponent` selector within the `AppComponent`, you add the element, `<app-item>`, which corresponds to the selector you defined for the component class to `app.component.html`.
Replace the current unordered list `<ul>` in `app.component.html` with the following updated version:

```html
<h2>
  \{{items.length}}
  <span> @if (items.length === 1) { item } @else { items } </span>
</h2>

<ul>
  @for (item of items; track item.description) {
  <li>
    <app-item (remove)="remove(item)" [item]="item"></app-item>
  </li>
  }
</ul>
```

Change the `imports` in `app.component.ts` to include `ItemComponent` as well as `CommonModule`:

```ts
@Component({
  standalone: true,
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrl: "./app.component.css",
  imports: [CommonModule, ItemComponent],
})
export class AppComponent {
  // …
}
```

The double curly brace syntax, `\{{}}`, in the `<h2>` interpolates the length of the `items` array and displays the number.

The `<span>` in the `<h2>` uses an `@if` and `@else` to determine whether the `<h2>` should say "item" or "items".
If there is only a single item in the list, the `<span>` shows "item".
Otherwise, if the length of the `items` array is anything other than `1`, the `<span>` shows "items".

The `@for` - Angular's control flow block, used to iterate over all of the items in the `items` array.
Angular's `@for` like `@if`, is another block that helps you change the structure of the DOM while writing less code.
For each `item`, Angular repeats the `<li>` and everything within it, which includes `<app-item>`.
This means that for each item in the array, Angular creates another instance of `<app-item>`.
For any number of items in the array, Angular would create that many `<li>` elements.

You can wrap other elements such as `<div>`, `<span`, or `<p>` within an `@for` block.

The `AppComponent` has a `remove()` method for removing the item, which is bound to the `remove` property in the `ItemComponent`.
The `item` property in the square brackets, `[]`, binds the value of `i` between the `AppComponent` and the `ItemComponent`.

Now you should be able to edit and delete items from the list.
When you add or delete items, the count of the items should also change.
To make the list more user-friendly, add some styles to the `ItemComponent`.

## Add styles to ItemComponent

You can use a component's style sheet to add styles specific to that component.
The following CSS adds basic styles, flexbox for the buttons, and custom checkboxes.

Paste the following styles into `item.component.css`.

```css
.item {
  padding: 0.5rem 0 0.75rem 0;
  text-align: left;
  font-size: 1.2rem;
}

.btn-wrapper {
  margin-top: 1rem;
  margin-bottom: 0.5rem;
}

.btn {
  /* menu buttons flexbox styles */
  flex-basis: 49%;
}

.btn-save {
  background-color: #000;
  color: #fff;
  border-color: #000;
}

.btn-save:hover {
  background-color: #444242;
}

.btn-save:focus {
  background-color: #fff;
  color: #000;
}

.checkbox-wrapper {
  margin: 0.5rem 0;
}

.btn-warn {
  background-color: #b90000;
  color: #fff;
  border-color: #9a0000;
}

.btn-warn:hover {
  background-color: #9a0000;
}

.btn-warn:active {
  background-color: #e30000;
  border-color: #000;
}

.sm-text-input {
  width: 100%;
  padding: 0.5rem;
  border: 2px solid #555;
  display: block;
  box-sizing: border-box;
  font-size: 1rem;
  margin: 1rem 0;
}

/* Custom checkboxes
Adapted from https://css-tricks.com/the-checkbox-hack/#custom-designed-radio-buttons-and-checkboxes */

/* Base for label styling */
[type="checkbox"]:not(:checked),
[type="checkbox"]:checked {
  position: absolute;
  left: -9999px;
}
[type="checkbox"]:not(:checked) + label,
[type="checkbox"]:checked + label {
  position: relative;
  padding-left: 1.95em;
  cursor: pointer;
}

/* checkbox aspect */
[type="checkbox"]:not(:checked) + label::before,
[type="checkbox"]:checked + label::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 1.25em;
  height: 1.25em;
  border: 2px solid #ccc;
  background: #fff;
}

/* checked mark aspect */
[type="checkbox"]:not(:checked) + label::after,
[type="checkbox"]:checked + label::after {
  content: "\2713\0020";
  position: absolute;
  top: 0.15em;
  left: 0.22em;
  font-size: 1.3em;
  line-height: 0.8;
  color: #0d8dee;
  transition: all 0.2s;
  font-family: "Lucida Sans Unicode", "Arial Unicode MS", Arial;
}
/* checked mark aspect changes */
[type="checkbox"]:not(:checked) + label::after {
  opacity: 0;
  transform: scale(0);
}
[type="checkbox"]:checked + label::after {
  opacity: 1;
  transform: scale(1);
}

/* accessibility */
[type="checkbox"]:checked:focus + label::before,
[type="checkbox"]:not(:checked):focus + label::before {
  border: 2px dotted blue;
}
```

## Summary

You should now have a styled Angular to-do list application that can add, edit, and remove items.
The next step is to add filtering so that you can look at items that meet specific criteria.

{{PreviousMenuNext("Learn_web_development/Core/Frameworks_libraries/Angular_styling","Learn_web_development/Core/Frameworks_libraries/Angular_filtering", "Learn_web_development/Core/Frameworks_libraries")}}
