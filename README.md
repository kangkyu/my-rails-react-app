# my-rails-react-app

My goal was to consume its own JSON of Rails by passing url in a way shows on this tutorial https://facebook.github.io/react/docs/tutorial.html#fetching-from-the-server

```jsx
ReactDOM.render(
  <CommentBox url="/api/comments" />,
  document.getElementById('content')
);
```

I didn't want to use `react-rails` this time and wanted not to touch controller for rendering components.
`react-rails` gem was tried at [kangkyu/try_react-rails_gem](https://github.com/kangkyu/try_react-rails_gem)

## Install & Run local

```sh
bower install
npm install
bundle install
rails server
```

## Notes

For this try-out app I simply follow [facebook/react](https://facebook.github.io/react/docs/tutorial.html) tutorial - and the tutorial starts with remote links of `react` `react-dom` `browser` `jquery` in html head tag.

```html
<head>
  <meta charset="utf-8" />
  <title>React Tutorial</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react-dom.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
</head>
```

I wanted to do it in Rails Assets style like this:

```js
//= require react/react
```

### React: from bower

+ https://www.codefellows.org/blog/5-ways-to-manage-front-end-assets-in-rails
+ https://coderwall.com/p/6bmygq/heroku-rails-bower
+ http://linhmtran168.github.io/blog/2014/02/28/using-bower-with-rails/

Setup `bower` and install react. In short, we need add a directory name to those three files:

```sh
.bowerrc
.gitignore
config/application.rb
```

For the directory name, I picked `vendor/assets/bower_components`.

```sh
# .bowerrc
{
  "directory": "vendor/assets/bower_components"
}

# .gitignore
vendor/assets/bower_components/

# config/application.rb
config.assets.paths << Rails.root.join('vendor', 'assets', 'bower_components')
```

Then install these two.

```sh
bower init
bower install --save react
bower install --save react-dom
```

### jquery

**jQuery** was already in Rails by default `gem 'jquery-rails'`.

Now, `react` `react-dom` `jquery` are ready.

### browser.js

+ [in-browser-jsx-transform](https://facebook.github.io/react/docs/tooling-integration.html#in-browser-jsx-transform) used here

`babel-core/browser` should be installed by `npm`.
Follow the steps of [this article](https://pawelgrzybek.com/fix-priviliges-and-never-again-use-sudo-with-npm/) and let's not use `sudo npm`.

```sh
npm install --save babel-core
```

```rb
# .gitignore
node_modules/

# config/application.rb
config.assets.paths << Rails.root.join('node_modules')
```

And then, require all of them in `application.js`

```js
app/assets/javascripts/application.js

//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require react/react
//= require react/react-dom
//= require babel-core/browser
```

## More..

pull out js code out of view file and move into a separate file `app/assets/javascript/scripts/example.js`

```html
<!-- single_page.html.erb -->
<script type="text/babel" src='scripts/example.js'></script>
```

didn't work. that link simply coming from "/script" route.

```
<script type="text/babel" src=<%= asset_path 'scripts/example.js' %>></script>
```

gave out an error.

```
Asset filtered out and will not be served: add `Rails.application.config.assets.precompile += %w( scripts/example.js )` to `config/initializers/assets.rb` and restart your server
```

followed instruction on the error message.

```rb
# config/initializers/assets.rb
Rails.application.config.assets.precompile += %w( scripts/example.js )
```

And it worked then.
