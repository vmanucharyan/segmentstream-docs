---
layout: page
section: ecommerce
title: "Product listing page"
date: 2020-04-13
order: 2
---

<ul class="page-navigation">
  <li><a href="#introduction">Introduction</a></li>
  <li><a href="#required-variables">Required variables</a></li>
  <ul>
    <li><a href="#page">page</a></li>
    <li><a href="#listing">listing</a></li>
    <li><a href="#cart">cart</a></li>
    <li><a href="#website">website</a></li>
    <li><a href="#user">user</a></li>
    <li><a href="#version">version</a></li>
  </ul>
  <li><a href="#example">Example</a></li>
</ul>

### <a name="introduction"></a>Introduction
------

A product listing page displays a subset of related products.

> A category page that contains a group of sub-categories that help the customer navigate deeper into the site - is **NOT** considered a product listing. On such pages, `digitalData.page.type` should be given the value of `content`. A small list of products on such a page is a list of `recommendations`, not a primary `listing`.

On the product category pages of the online store, the following objects must be defined: `listing`, `page`, `website`, `user`, `cart`, `version`.

## <a name="required-variables"></a>Required variables
------

### <a name="page"></a>page
You need to define only `page.type` variable in the `digitalData.page` object. All other variables are either optional or will be automatically filled by the SegmentStream SDK.

[More about the **page** object](/digitaldata/page)

Example:
```javascript
  window.digitalData = {
    ...,
    page: {
      type: 'listing',
      category: 'Category Listing'
    },
    ...
  }
```

>There can be several different types of listings on the site: new arrivals, discounted goods, brand-specific products and so on. Use the `page.category` variable to separate such lists: 'New Arrivals Listing', 'Sales Listing', 'Brand Listing', etc.

### <a name="listing"></a>listing
The `digitalData.listing` object must be declared and filled on any page that has `digitalData.page.type` = `listing`.

[More about the **listing** object](/digitaldata/listing)

Example:
```javascript
window.digitalData = {
  ...,
  listing: {
    listName: "category",
    listId: "main",
    categoryId: "125656",
    category: ['Clothing','Skirts','Long'],
    items: [
      ...,
      {
        id: "1234567890",
        url: "http://website.com/product.html",
        imageUrl: "http://website.com/image.png",
        thumbnailUrl: "http://website.com/image_thumb.png",
        name: "Big Boots",
        description: "Product description",
        manufacturer: "Timberland",
        category: ["Footwear","Boots"],
        currency: "GBP",
        unitPrice: 60,
        unitSalePrice: 50,
        skuCode: "TBL6065RW"
      },
      ...
    ],
    sortBy: "price_asc",
    resultCount: 20,
    pagesCount: 13,
    currentPage: 2,
    layout: "grid"
  },
  ...
}
```

### <a name="website"></a>website
You need to declare and fill in only 6 variables in the `digitalData.website` object. The following 3 variables are required: `website.type`,` website.currency`, `website.environment`. The remaining variables depend on the characteristics of your site.

[More about the **website** object](/digitaldata/website)

Example:
```javascript
  window.digitalData = {
    ...,
    website: {
      region: "London",
      regionId: "11",
      type: "desktop",
      language: "en-gb",
      currency: "GBP",
      environment: "production"
    },
    ...
  }
```

### <a name="user"></a>user
The composition of the `digitalData.user` object strongly depends on the requirements of the project. We recommend that you fill at least the following variables: `userId`, `user.email`, `user.isLoggedIn`, `user.firstName`, `user.isSubscribed`

>If you do not have information about a particular property of a visitor, do not declare the variable. For example: you do not know if the visitor is subscribed to the email-list.<br/>
**Correct**: do not declare the variable `digitalData.user.isSubscribed`.<br/>
**Wrong**: declare a variable and assign it a value of FALSE.

[More about the **user** object](/digitaldata/user)

Example:
```javascript
window.digitalData = {
  ...,
  user: {
    firstName: "John",
    userId: "4638mn1",
    email: "jdoe@example.com",
    isLoggedIn: true,
    isSubscribed: false
  },
  ...
}
```

### <a name="cart"></a>cart
The `digitalData.cart` object must be declared and filled when loading each page of the site.

If the user's cart is empty fill the object as described in the [cart object description](/digitaldata/cart#0)

[More about the **cart** object](/digitaldata/cart)

Example:
```javascript
window.digitalData = {
  ...,
  cart: {
    id: "CART2203",
    currency: "GBP",
    subtotal: 100,
    total: 105,
    lineItems: [
      ...,
      {
        product: {
          id: "1234567890",
          url: "http://website.com/product.html",
          imageUrl: "http://website.com/image.png",
          thumbnailUrl: "http://website.com/image_thumb.png",
          name: "Big Boots",
          description: "Product description",
          manufacturer: "Timberland",
          category: ["Footwear","Boots"],
          currency: "GBP",
          unitPrice: 60,
          unitSalePrice: 50,
          skuCode: "TBL6065RW"
        },
        quantity: 2,
        subtotal: 100
      },
      ...
    ]
  },
  ...
}
```

### <a name="version"></a>version
The `digitalData.version` variable must be declared and filled when loading each page of the site.

[More about the **version** variable](/digitaldata/standard-version)

Example:
```javascript
window.digitalData = {
  ...,
  version: '1.1.3',
  ...
}
```

## <a name="example"></a>Example
------
In the end, your code will be similar to:
```javascript
window.digitalData = {
  listing: {
    listName: "category",
    listId: "main",
    categoryId: "125656",
    category: ['Clothing','Skirts','Mini'],
    items: [
      {
        id: "1234567890",
        url: "http://website.com/product.html",
        imageUrl: "http://website.com/image.png",
        thumbnailUrl: "http://website.com/image_thump.png",
        name: "Leather skirt",
        description: "Description",
        manufacturer: "Gucci",
        category: ['Clothing','Skirts','Mini'],
        currency: "GBP",
        unitPrice: 100,
        unitSalePrice: 100,
        skuCode: 'TBL6065RW'
      }
    ],
    sortBy: "price_asc",
    resultCount: 20,
    pagesCount: 13,
    currentPage: 2,
    layout: "grid"
  },
  page: {
    type: 'listing',
    category: 'Category Listing'
  },
  website: {
    type: "desktop",
    currency: "GBP",
    environment: "production"
  },
  user: {
    firstName: "John",
    userId: "4638mn1",
    email: "jdoe@example.com",
    isLoggedIn: true,
    isSubscribed: false
  },
  cart: {
    id: "CART2203",
    currency: "GBP",
    vouchers: [
      "MYVOUCHER1"
    ],
    voucherDiscount: 10,
    tax: 10,
    shippingCost: 5,
    shippingMethod: "Delivery",
    subtotal: 100,
    total: 95,
    lineItems: [
      {
        product: {
          id: "1234567890",
          url: "http://website.com/product.html",
          imageUrl: "http://website.com/image.png",
          thumbnailUrl: "http://website.com/image_thumb.png",
          name: "Big Boots",
          description: "Product description",
          manufacturer: "Timberland",
          category: ["Footwear","Boots"],
          currency: "GBP",
          unitPrice: 60,
          unitSalePrice: 50,
          skuCode: "TBL6065RW"
        },
        quantity: 2,
        subtotal: 100
      }
    ]
  },
  version: '1.1.3'
}

/**
 * SegmentStream JavaScript SDK snippet should be
 * placed after the digitialData object definition
 */
```

>For convenience, we did not list the repeating elements of the `items` and `lineItems` arrays.
