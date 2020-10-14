# About this Project

We use this project to manage technical documentation for the Goodshuffle wishlist.

## Setup

Install [Hugo](https://gohugo.io/getting-started/usage/).

```
brew install hugo
```

Init the 'book' theme

```
 git submodule update --init
```

Run the server.

```
hugo server --minify --theme book
```

Make any edits you'd like to the docs.

## Deploy

Netlify will automatically handle the build and deploy process.

Merge your feature branch into `staging` to deploy to the test site for testing and review.

Merge `staging` into master to deploy to the public developer [documentation site](https://docs.goodshuffle.dev/).

