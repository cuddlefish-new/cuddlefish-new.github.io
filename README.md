# Cuddlefish
Cuddlefish is a rapid prototyping environment for designing-in-browser.

Table of Contents:

1. [Team Coding Philosophy](https://github.com/cuddlefish-new/cuddlefish-new.github.io#team-coding-philosophy)
2. [Getting Cuddlefish Running On Your Machine](https://github.com/cuddlefish-new/cuddlefish-new.github.io#getting-cuddlefish-running-on-your-machine)
3. [Contributing to Cuddlefish](https://github.com/cuddlefish-new/cuddlefish-new.github.io#contributing-to-cuddlefish)
4. [Submitting A Pull Request](https://github.com/cuddlefish-new/cuddlefish-new.github.io#submitting-a-pull-request)
5. [Building & Deploying Cuddlefish](https://github.com/cuddlefish-new/cuddlefish-new.github.io#building--deploying-cuddlefish)
6. [Using Partials](https://github.com/cuddlefish-new/cuddlefish-new.github.io#using-partials)
7. [Using Bootstrap Modules (Helpers)](https://github.com/cuddlefish-new/cuddlefish-new.github.io#bootstrap-helpers)
8. [SCSS](https://github.com/cuddlefish-new/cuddlefish-new.github.io#scss)


## Team Coding Philosophy

Below is a list of coding considerations when contributing to Cuddlefish.

1. **Small CSS**: Keep our CSS files small and specific with the goal of only including files that address either reusable/utility classes or specific components (or widgets). We'll use the .SCSS flavor of the preprocessor SASS.
  ```
  cuddlefish/
    +-- stylesheets
      +-- plugins
      ¦   +-- animate.css
      ¦   +-- fonts.css
      ¦   +-- grid.css
      ¦   +-- reset.css
      +-- globals
      ¦   +-- utility-classes.scss
      ¦   +-- variables.scss
      +-- components
      ¦   +-- media-object.scss
      +-- widgets
          +-- hero-slideshow-billboard.scss
          +-- super-fun-gallery.scss
          +-- tabbed-list.scss
  ```

2. **Be Specific**: We use [the BEM naming convention](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) to target elements in our HTML documents.

  ```
  <div class="block__element">
    <div class="block__element--modifier"></div>
  </div>
  ```
  Targeting elements this way addresses most of the concerns listed in [these best practices](https://github.com/sezgi/CSS-Best-Practices) around writing scalabale and reusable CSS.
3. **Practice Object-Oriented CSS**.
4. **Always Be Iterating**: Make small strides to iterate on our CSS Styleguide, as of now, here are some coding constraints we've agreed on as team:
  + Grouping CSS properties logically, or by how they affect the DOM (Document Object Model), in this order: 
    1. **Display properties** (or things that affect the box model of an element or object)
    2. **Type** (things that affect how fonts are displayed and positioned)
    3. **Visual Styles**
    4. **Animations and/or element transitions**
    
    An example: 
    ```
    .block__element--modifier {
      display: block;
      height: $height; 
      width: $width;
      box-sizing: border-box;
      margin: 0 auto;
      
      color: $color;
      font-family: $Open-Sans;
      font-size: 16px; /* Use pixels to specify an element's font-size */
      line-height: 1.5; /* Use integers to specify an element's line-height */
      text-align: center;
      
      background: $bg-color url('images/bg.jpeg');
      background-color: $bg-color;
      background-image: url('images/bg.jpeg');
      background-position: center center;
      background-repeat: no-repeat;
      background-size: cover;
      border: 1px solid $border-color;
    }
    ```
5. **Use Modern Browser fallbacks or vendor prefixes only.**
    +  Let the dev team worry about granular cross-browser compatibility. We should be spending as much of our time as possible on designing-in-the-browser. Keep in mind, though, that you may need to include *certain* vendor prefixes so people can properly view your design progress in the *modern browser* of their choice. Probably the most important of these properties is `box-sizing`, which we can create an `@include` for in our CSS so that we don't have repeat ourselves too often.


      An example: 

      ```
      /* Without an @include (plain CSS) */
      
      .block__element--modifier {
        -moz-box-sizing: border-box;
        -webkit-box-sizing: border-box;
        box-sizing: border-box;
      }
      
      /* OR, with an @include (SCSS) */
      
      .block__element--modifier {
         @include box-sizing(border-box);
      }
      ```

## Getting Cuddlefish running on your machine
First, let's install Middleman (the framework Cuddlefish is built on top of) onto your machine.

```
$ gem install middleman
```
Next, to download or clone the project down and run it on your machine:

```
$ cd folder_where_you_want_cuddlefish_to_live
$ git clone https://github.com/cuddlefish-new/cuddlefish-new.github.io.git cuddlefish
$ cd cuddlefish
```

To get started dev-ing:

```
$ git pull
$ bundle install
$ bundle exec middleman server
$ open http://localhost:4567/
```
`bundle install` will install all of our apps dependencies on your machine, `bundle exec middleman server` will start a local server so that you can view pages in your browser, and the open script will open the app in your browser.

## Contributing to Cuddlefish

The `master` branch will be our "base" branch and the one that we deploy to "production". Our `master` branch should always be clean or unbroken and ready to deploy at any time.

To contribute to the project you'll create a branch off of `master`, make your changes, & submit a [pull request](https://guides.github.com/introduction/flow/) comparing your branch to `master`. 

By default when you clone the project, you will be on the `master` branch. To check to make sure you're on this branch run: 

```
$ git status
```
You should see the terminal return something like:
```
On branch master
Your branch is up-to-date with 'origin/master'.
```

To start contributing to Cuddlefish, create a new branch. Make sure you're branching off of `master` so we can merge your changes in later. If you need to switch to the `gh-pages` branch, run: 
```
$ git checkout master
$ git pull origin master
```
And then to create a new branch:
```
$ git checkout -b your-branch-name
```
You should try to name your branch after an issue you're addressing/fixing or after the widget you're designing. 

Once you make changes you want to commit to your branch push your branch up to GitHub:

```
$ git push origin your-branch-name
```

## Submitting a Pull Request

If you have a branch going with changes that you're ready to have pulled or merged into our master/base branch (`master`), create a pull request on GitHub comparing your changes with the base branch. Let's make the rule that for now you need to have at least one other person review your code before it can be merged into the base and deployed. This also applies to any refactoring as well, not only new widgets designs.

## Building & Deploying Cuddlefish

While on `master`:

```
$ middleman build && middleman deploy
```

## Using Partials

If you're contributing a reusable component or object, consider creating a "partial" (partials/_price-block.html.erb) instead of a view (i.e. price-block.html.erb). Here is the syntax for calling a partial inside of an erb view:

```<%= partial "partials/price-block" %>```

For more specifics on using partials with middleman, refer to the documentation [here](https://middlemanapp.com/basics/partials/).

## Bootstrap Helpers
In order to trigger a JS modal or notice, we're using Bootstrap Helpers in our project. We'll trigger one of these elements by writing an "erb" tag like the one below.
```
<%= alert_box 'You accepted the Terms of service.', dismissible: true %>
```
You can find the full documentation and examples [here](http://fullscreen.github.io/bh/).

## SCSS
We're using the SCSS flavor of SASS, the documentation can be found [here](http://sass-lang.com/guide).
