Warning: Each child in an array or iterator should have a unique "key" prop. Check the render method of `CommentList`. See https://fb.me/react-warning-keys for more information.

http://facebook.github.io/react/docs/multiple-components.html#dynamic-children

--

`asset_path` helper

http://guides.rubyonrails.org/asset_pipeline.html#coding-links-to-assets

```rb
# assets.rb
Rails.application.config.assets.precompile += %w( scripts/example.js )
```

```html
<!-- single_page.html.erb -->
<script type="text/babel" src=<%= asset_path 'scripts/example.js' %>></script>
```