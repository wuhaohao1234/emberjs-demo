# ember-demo

This README outlines the details of collaborating on this Ember application.
A short introduction of this app could easily go here.

## install ember-cli

```sh
npm install -g ember-cli
```

## create a new app

```sh
ember new ember-demo
```

## write somm html in a template

in app/template/applaction.hbs

```html
<h1>hello world</h1>

{{outlet}}
```

## define route

```shell
ember generagte route scientists
```

edit app/template/scientists.hbs

```html
<h2>List of Scientists</h2>
```

in browser open http://loalhost:4200/scientists

edit app/template/scientists.js

```js
import Route from "@ember/routing/route";

export default class ScientistsRoute extends Route {
  model() {
    return ["Marie Curie", "Mae Jemison", "Albert Hofmann"];
  }
}

```

edit app/template/scientists.hbs

```html
<h2>List of Scientists</h2>

<ul>
  {{#each @model as |scientist|}}
    <li>{{scientist}}</li>
  {{/each}}
</ul>
```

## create component people-list

```sh
ember generate component people-list
```

edit app/components/people-list.hbs

```html
<h2>{{@title}}</h2>

<ul>
  {{#each @people as |person|}}
    <li>{{person}}</li>
  {{/each}}
</ul>
```

scientists use people-list

edit app/template/scientists.hbs
```html
{{!-- <h2>Scientists</h2>
<ul>
  {{#each @model as |scientist|}}
    <li>{{scientist}}</li>
  {{/each}}
</ul> --}}
<PeopleList 
  @title="people"
  @people={{@model}}
/>
{{outlet}}
```

edit app/components/people-list.hbs

```html
<h2>{{@title}}</h2>

<ul>
  {{#each @people as |person|}}
    <li>
      <button type="button">{{person}}</button>
    </li>
  {{/each}}
</ul>
```

edit app/components/people-list.js

```js
import Component from '@glimmer/component';
import { action } from '@ember/object';

export default class PeopleListComponent extends Component {
  @action
  showPerson(person) {
    alert(`The person's name is ${person}!`);
  }
}
```

edit app/components/people-list.hbs

```html
<h2>{{@title}}</h2>

<ul>
  {{#each @people as |person|}}
    <li>
      <button type="button" {{on 'click' (fn this.showPerson person)}}>{{person}}</button>
    </li>
  {{/each}}
</ul>
```

## build production

```shell
ember build --environment=production
```