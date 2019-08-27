# Unique things about this project

## Use

Add new entries in content subdirectory (such as `blog`). Use front matter for changing fields related to post:

| Field | Usage |
| ----- | ----- |
| title | |
| author** | |
| date | creation date of post (use `lastmod` if post is modified after its original publication) |
| tags** | topics addressed in blog |
| summary | content to show when blog is summarized, such as in a list (if not provided, will use beginning of blog content) |
| thread** | name of series post belongs to |
| lastmod** | date last modified when different from creation date (other posts belonging to same series will be listed after post) |
| comments | true to allow comments, any other value will cause comments not to show |
| discussionId | alternate discussion id for comment system (By default, comments are tied to filename -- this should allow URL changes without affecting the comment system) |

** Indicates specific logic (mostly in layouts/partials) to render optional field appropriately


## Design

### Separation of Concerns

While there are limits to how well this separation can be maintained in different themes, an attempt was made to separate function of site (layouts/partials) from theme -- in such a way that minimal changes should be needed in a new theme to implement the site structure.

### CSS Switching for Solarized theme

For the main theme (A slightly modified open source Solarized theme), there is CSS switching between light/ dark modes by clicking on a link.

### Icon Switching

SVG icons are used, and there is a way to swap out the icon family in the config.toml.

### New Elements

   * Author
   * Date last updated
   * Tags
   * Thread (Posts related by series)
   * External commenting system (ie, Talkyard)

TODO: Visible anchor link for headings