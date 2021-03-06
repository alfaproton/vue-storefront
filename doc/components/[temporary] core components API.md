# Core components API

Temporary file for core components API. List of props, public methods and data that are available to use via mixin insertion.
In case of injectable components (like modal) or the ones triggered by Vuex actions you should write them down also. Feel free to write some description/new api proposal for each docummented component.

## AddToCart
This component represents a single button that when pressed adds a product to cart. Right now this component is used on Product page only.
### Props
`product` - An instance of a product  
### Data
No data
### Methods
`addToCart (product)` - Dispatches 'cart/addItem' action and passes a product instance as a parameter.  
**Parameters:**  
*product* - An instance of a product

## Breadcrumbs
This component represents a hierarchy of the current page in relation to the application's structure. It is used in Product, Category, My Account and Compare pages.
### Props
`routes` - An array of route objects, each representing name and path to a parent page.  
`activeRoute` - A name of the current page
### Data
No data
### Methods
No methods

## ColorButton
This components represents a button that is used for visualizing different options, specifically product filters. It is used on category's Sidebar and Product pages.
### Props
`label` - label that is shown on the component button.  
`id` - identifier that unifies an option among others in array.  
`code` - a name of an option that the component is being used to represent (currently 'color').  
`context` - a name of an entity that the component belongs to (currently one of 'category' or 'product').
### Data
No data
### Methods
No methods

## Loader
This component is used for visualizing loading process, when something is happening in the background. It is currently used when account is being registered, password is being reset and user is logging in. 
### Props
No props
### Data
`message` - A message that is shown while loading process is on.  
`isVisible` - Computed property which is equal to UI-store's *loader* property. This prop defines whether to show or hide the spinner.
### Methods
`show (message = null)` - Sets message property and calls UI-store mutation 'ui/setLoader', which causes a spinner to show up.  
**Parameters:**  
*message* - A text that is shown when loading process is on.  

`hide` - Calls UI-store mutation 'ui/setLoader', which hides a spinner.  
**Parameters:**  
No parameters
### Hooks
#### Mounted
Two listeners are defined:  
`'notification-progress-start'` - calls *show* method.  
`'notification-progress-stop'` - calls *hide* method.

## Logo
This component is intended to serve an image of an application's logo and to navigate the user to a Home page when the logo is pressed.
### Props
No props
### Data
No data
### Methods
No methods

## Newsletter popup (should be using modal)
Shows popup modal window where user can enter his newsletter subscription preferences, currently only email address. This components is used in a Footer page.
### Props
No props
### Data
No data
### Methods
`closeNewsletter` - Closes newsletter popup modal window by calling UI-store mutation 'ui/setNewsletterPopup'.

## Notification

Shows notifications after some actions being performed in shop. There are four types of notifications: success, error, warning and info.

### Props
No props 

### Data
`notifications` - An Array of notifications that should be currently displayed

### Methods
`action(action, id)` - Performs an `action` defined as String on notification with passed `id` - usually the action is `close`. Actions are defined in Notification component. Current Notification object schema:
```json
{
    // Choose one
    "type": "info/success/error/warning",
    "title": "Lorem ipsum",
    "action1": {
        "label": "OK",
        "action": "close"
    },
    // Optional param
    "action2": {
        "label": "NO",
        "action": "close"
    },
    // Optional param, if its empty TTL is 5s
    "timeToLive": 10
}
```

### Events

`('notification', notificationObject)` - takes notification object and adds it to Notification array, then the nnew notification is displayed

## OfflineBadge
When there's no active internet connection, shows notification about getting offline at the bottom of the screen.
### Props
No props
### Data
`isOnline` - defines if there is an active internet connection
### Methods
No methods
### Hooks
#### Mounted
Sets isOnline data property and defines two event listeners:  
`'online'` - sets *isOnline* data property to true.  
`'offline'` - sets *isOnline* data property to false.

## Overlay
This component is used to shadow parts of the screen that are left after opening modal windows, like WishList or Cart.
### Props
`isVisible` - computed property that is equal to *overlay* property of UI-store. Defines whether to shadow parts of the screen or not.
### Data
No data
### Methods
`close` - calls UI-store mutation 'ui/setOverlay' and sets its *overlay* property to *false*.
### Hooks
#### beforeCreate
Adds *no-scroll* property to document, making shadowed parts of the screen unscrollable.
#### destroyed
Removes *no-scroll* property from document.

## PriceButton
Represents one of the options on Category page. Shows price range and allows uesr to choose one of the ranges.
### Props
`content` - text that shows the price range  
`id` - unique identifier of the option  
`code` - options' code, equals to 'price'  
`from` - minimum value of the price range  
`to` - maximum value of the price range  
`context` - a name of an entity that the component belongs to (currently 'category')
### Data
No data
### Methods
No methods

## ProductAttribute
Shows attributes that a specific product has. Used on Product Page.
### Props
`product` - reference to product that the attribute belongs to  
`attribute` - attribute itself  
`emptyPlaceholder` - a string that is shown if an attribute has no value
### Data
`label` - name of an attribute
`value` - attribute's value(-s)
### Methods
No methods
### Hooks
#### beforeMount
Extracts attribute's label and value(-s) from *product* and *attribute* properties.

## ProductLinks
If product is grouped (which means it consists of several products) this component shows list of compound products. Used on Product page.
### Props
`products` - array of compound products of a given product
### Data
No data
### Methods
No methods

## ProductListing
Shows given array of products on a page in a given number of columns. Used on Category and Home pages, and also on Related block.
### Props
`product` - array of products to show  
`columns` - number of columns to display on a page. Each product is displayed with ProductTile component.
### Data
No data
### Methods
No methods

## ProductSlider
Shows product tiles slider. Used in Collection component in *default* theme. 
### Props
`title` - a title of a slider  
`products` - an array of products to show in a slider  
`config` - and object that defines configuration of a slider, like number of tiles to show on a page, pagination and looping.
### Data
No data
### Methods
No methods

## ProductTile
Shows a product in a compact way when several products are shown on one page. Used in many places, such as Home page, Search panel, 404 page and so on.
### Props
`product` - a specific product  
`thumbnail` - a computed property that represents a smaller image for the product to show in this component. *The size of an image is hard-coded in this property, it might be better to keep dimensions in a config file.*
### Data
No data
### Methods
No methods

## SizeButton
Represents one of the options of a product, namely product's size. Used on Category and Product pages.
### Props
`label` - a string that represents the size  
`id` - unique identifier of the size  
`code` - a code name of an option, which is 'size'  
`context` - a name of an entity that the component belongs to (currently one of 'category' or 'product')
### Data
No data
### Methods
No methods

## Tooltip
Shows an informational icon and hint when focused on that icon. Used on My Account and Checkout pages.
### Props
No props
### Data
No data
### Methods
No methods

## ValidationError
This was supposed to show a validation error message, but is not used anywhere. *Has to be deleted*
### Props
`message` - a text that explains the error
### Data
No data
### Methods
No methods

# Core pages

## Category

### Props
No props
### Data
`pagination` - an object that defines two settings:  
    1. *number* of product items to load per page, currently set to 50;  
    2. *offset* that probably defines which page has been last loaded, currently set to 0 and doesn't change anywhere.
`filterSet` - a set of filters that user has defined on Category page.  
`products` - computed property that return a list of product items of current category from the Vuex store.  
`isCategoryEmpty` - computed property that return true if product list of current category is empty.  
`category` - computed property that return current category from the Vuex store.  
`aggregations` - computed property *that is not used*.  
`filters` - a set of all available filters for current category from the Vuex store.  
`breadcrumbs` - breadcrumbs for current category from the Vuex store.
### Methods
`fetchData ({ store, route })` - prepares query for fetching a list of products of the current category and dispatches *'product/list'* action that extracts that list.  
**Parameters**  
*{ store, route }* - an object consisting of the Vuex store and global router references.  

`validateRoute ({ store, route })` - this method is called whenever the global *$route* object changes its value. It dispatches *'category/single'* action to load current category object and then calls *fetchData* method to load a list of products that relate to this category.  
**Parameters**  
*{ store, route }* - an object consisting of the Vuex store and global router references.
### Hooks
#### asyncData
Since the app is using SSR, this method prefetches and resolves the asyncronous data before rendering happens and saves it to Vuex store. Asyncronous data for Category page is list of all categories, category attributes and list of products for each category.
#### beforeMount
*'filter-changed-category'* event listener is initialized. *Although this event is not triggered anywhere.*
#### beforeDestroy
*'filter-changed-category'* event listener is removed.

## Checkout

### Props
No props
### Data
`stockCheckCompleted` - a boolean prop that shows if all products in cart (if any) have been checked for availability (whether they are in stock or not).  
`stockCheckOK` - a boolean prop that shows if all products in cart are in stock.  
`orderPlaced` - a boolean prop that is set to true after *'order-after-placed'* event has been triggered, defining a placement of order.  
`activeSection` - an object that consists of 4 boolean props: *personalDetails*, *shipping*, *payment* and *orderReview*, - that define which section of Checkout page is currently active. At any point of time only one section can be active.  
`order` - an order object, that consists of all necessary order information that will be sent to the backend to place it.  
`personalDetails` - an object that contains personal details part of the Checkout page.  
`shipping` - an object that contains shipping details part of the Checkout page.  
`payment` - an object that contains payment details part of the Checkout page.  
`orderReview` - *this prop is not used*  
`cartSummary` - this prop is supposed to be filled after *'checkout.cartSummary'* event has been triggered. *But this event is not triggered anywhere, therefore this prop currently has no usage.*  
`validationResults` - an object that keeps validation result of 3 child components: Personal Details, Shipping Details and Payment Details. *Currently all the validation happens within those 3 child components and there's no need to store the result in a parent component. I think is prop is redundant.*  
`userId` - this new user ID is returned by child OrderReview component if a user registers a new account at checkout. It is then sent to the backend to bind an order to the user.  
`isValid` - this boolean computed property defines if an order can be placed. If there's any validation error within any child component or *stockCheckOK* prop is not true, this returns false and an order won't be placed.  
### Methods
`checkConnection (status)` - checks if there's an active internet connection. If not, fires a notification.  
**Parameters**  
*status* - a boolean parameter that defines if there's an active internet connection.  

`activateSection (sectionToActivate)` - sets *sectionToActivate* named section in *activeSection* prop object to true and all others to false.  
**Parameters**  
*sectionToActivate* - a name of a section that needs to be activated.  

`prepareOrder ()` - returns an order object that will be sent to the backend.  

`placeOrder ()` - if *isValid* prop is true dispatches *'checkout/placeOrder'* action which will place the order, otherwise fires a notification about existence of validation errors.  

`savePersonalDetails ()` - dispatches *'checkout/savePersonalDetails'* action which will save checkout personal details information (from *personalDetails* prop) to the Vuex store.  

`saveShippingDetails ()` - dispatches *'checkout/saveShippingDetails'* action which will save checkout shipping details information (from *shipping* prop) to the Vuex store.  

`savePaymentDetails ()` - dispatches *'checkout/savePaymentDetails'* action which will save checkout payment details information (from *payment* prop) to the Vuex store.
### Hooks
#### created
Defines several event listeners to communicate with child components. For example, *'checkout.personalDetails'* event listener to receive personal details information from PersonalDetails child component and activate next section of the Checkout page (which is shipping details).
#### beforeMount
Checks if cart is not empty. If it is, then a notification is fired. Otherwise, sets promises that will check availability of the products from the cart and if they are all in stock.
#### destroyed
Removes all event listeners that were previously defined in *created* hook.
