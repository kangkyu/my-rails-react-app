# my-rails-react-app

My goal was to consume its own JSON of Rails by passing url in a way shows on this tutorial https://facebook.github.io/react/docs/tutorial.html#fetching-from-the-server

```
ReactDOM.render(
  <CommentBox url="/api/comments" />,
  document.getElementById('content')
);
```

I didn't want to use `react-rails` this time and wanted not to touch controller for rendering components.

https://github.com/kangkyu/my-rails-react-app

### Install & Run local

```
npm install
bundle install
rails server
```

### Notes

For a try-out, this app simply follows https://facebook.github.io/react/docs/tutorial.html

the tutorial starts with remote links of `react` `react-dom` `browser` `jquery` in html head tag.

```
<head>
  <meta charset="utf-8" />
  <title>React Tutorial</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react-dom.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
</head>
```

https://www.codefellows.org/blog/5-ways-to-manage-front-end-assets-in-rails
https://coderwall.com/p/6bmygq/heroku-rails-bower
http://linhmtran168.github.io/blog/2014/02/28/using-bower-with-rails/

Setup `bower` and install these two. but not `babel-core/browser`

```
bower install --save react
bower install --save react-dom
```

Add directory name to those three files:

```
.bowerrc
.gitignore
config/application.rb
```

For directory name I picked `vendor/assets/bower_components`.

```
# .bowerrc
{
  "directory": "vendor/assets/bower_components"
}

# .gitignore
vendor/assets/bower_components/

# config/application.rb
config.assets.paths << Rails.root.join('vendor', 'assets', 'bower_components')
```

`react` `react-dom` `jquery` are ready. (**jQuery** was already in Rails by default `gem 'jquery-rails'`)

```
npm install --save babal-core
```

`babel-core/browser` should be installed by `npm`

```
# .gitignore
node_modules/

# config/application.rb
config.assets.paths << Rails.root.join('node_modules')
```

And then, require all of them in `application.js`

```
app/assets/javascripts/application.js

//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require react/react
//= require react/react-dom
//= require babel-core/browser
```
