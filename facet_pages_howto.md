# Facet subpages

We want to add individual pages for facets like `keywords`.

We can use the `facet_page_layout` to create new pages for these keywords. I've included an example page under `pages/docs_by/keywords` to demonstrate how this new layout can be used.

`pages/docs_by/keywords/freedom.md`
```
---
layout: facet_page_layout
gallery: True
field: keywords
value: 'freedom'
---

Sample page with a description about the 'freedom' keyword
```

The front matter tells Jekyll to use the new layout, enables the gallery view, and tells the layout about which keyword and value we are interested in displaying.

* `field` which column of the CSV is being used for the facet view. Set to "keywords" here
* `value` which facet value we'll display. Set to "freedom" here

The layout will add a list of all available keywords pages, the content of the `freedom.md` page, and will show a subgallery of only those documents that have the word "freedom" in the "keywords" column of the CSV


## New Example

If you want a page describing the **"marronage"** keyword, create a new markdown document in the `pages/docs_by/keywords/` folder. Keep the field as "keywords" but set the value to "marronage". The new page should look similar to:

`pages/docs_by/keywords/marronage.md`
```
---
layout: facet_page_layout
gallery: True
field: keywords
value: 'marronage'
---

Your new description would go here
```

Once the website has been built by Jekyll, a new link will show up in the `by_keywords` page, so if you navigate to `http://localhost:4000/keywords/pages/docs_by/by_keyword`, a new link for the "marronage" page should appear.

## Gallery bug

I have included a partial workaround to a bug I saw in the `gallery.html` component. While the component parses the CSV column to generate a list of facets to select with checkboxes, it does not do the same parsing when you want to immediately render a subset gallery with a predefined value. Instead, to get a match, you would have had to used the full value of a column, which would have included the whole comma delimited set of keywords.

My workaround simply matches all rows where the value of interest is found within the correct column. In this way, it will be over-eager in what documents it fetches. For example, if you want a gallery showing the facet "freedom", this workaround will accidentally also match "freedom suit".

Some work needs to be done in the future to correct this behavior.

# Note

* I don't quite know how this would play with date ranges yet.
