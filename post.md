#### 1. Origin of LOC
The main goal in any type of development is to have as much code as possible to be light weight, efficient, and reusable. CSS is a very unstructured language that allows one to create the exact same end piece through many different facets. As a result of CSS being so unstructured, many developers typically end up hitting a wall after creating months of style changes. To fix this, many have relied very heavily on popular css frameworks like Bootstrap, but still end up issues due to not having a standard in place when further developing. There are a lot of ideas out there on how to build your own internal framework for the UI, and how to integrate your own into a pre-exisitng one. I personally do not find it to be beneficial to create everything on your own, unless you have a standard in place. I know there are some methodologies out there for CSS like BEM, but honestly I kind of got tired of sorting through a massive amount of enterprise css framworks on consulting projects; so I came up with my own css naming convention called "LOC".

LOC stands for Level-Object-Component, and is a pretty flexible CSS naming convention. The benefit of LOC is where you can look at a template and know how the styles are being applied; like is it on a global scale or flow specific area. LOC helps resolve many common development team issues:

 - Standarizing development practices among internal and external development teams
 - A better understanding of what styles are being applied in the templates/ HTML pages
 - Faster Agile development of new and older features through tracing styles back to files without having to search
 - Creating reusable code that helps cut down on file size, and how much to maintain during development

#### 2. Setting Up SCSS Config File:
When creating your own internal CSS responsive framework it is smart to have a file that controls the entire theme of the application; like font styles, layout backgrounds, borders, and branding specific themes. This will provide great diversity in your development where you can restructure things on the fly without any headaches of tracking down crap.

```scss
/* Language PrePocesser: SASS */
$font_size01: 12px;
$font_size02: 14px;
$font_size03: 16px;
$font_size04: 18px;

/* Font Weights */
$font_weight01: 300;
$font_weight02: normal;
$font_weight03: bolder;

/* Branding Colors */
$brand_color: #555;
$brand_color-light: lighten($brand_color, .1);
$brand_color-darken: darken($brand_color, .1);

/* Layout Colors */
$layout_color01: #ffffff;
$layout_color02: #f4f4f4;
$layout_color03: #eeeeee;
$layout_color04: #aaa;

/* Border Colors */

/* Border Radius */


/* Tooltip Styles */
/* Modal Styles */
```
You will also will want to have a mixins file where you can reuse functions that are explicit to your application; like margins, padding, and creating widget bodies.

#### 3. LOC's Basic Ruleset
LOC has a simple set of rules to follow that allows developers to pick up quite quickly to use.
- A parent can only be applied 2 deep in HTML markup children; like parent -> direct decendant -> direct decendant's child. This helps cut down on the bulk and overuse of class tree fluff
- A new class that isn't affiliated with the current structure that it is in must always declare the level in which it is being invoked withing the markup; like is it global(g), flow specific(f), or flow-module(fm).
- CSS/SCSS/LESS file structure needs to be broken out into partials resembling parent-level structure
- Classes from a group should not inherit other component styles from other groups in order to keep modularity.

##### Global Level:
Examples: navigation, sidemenu, content containers, layout boxes used across the site

##### Flow Specific: 
Marketing pages, product listing pages, contact us, and etc...

##### Flow-Module:
This will be content that resides within the flow pages; like a sells listing popup that only exist on the product listing pages



```css
    /* Compiled SASS to CSS
     * BREAKDOWN: g(global) - box0(layout Initial*/
    .g-box01{
        padding: 20px 10px;
        width: 50%;
    }
```

#### 4. Flow/ Module Specific Layout
A flow specific item would be like a widget or something. For example, lets say that you are developing a twitter feed to have on the front of your web application that displays the latest in what is trending.

```scss
    /* 
     * DECLARING: Proucts Page level
     ************************************************************************ */
     .f-products{
        margin: 5px 0;
        padding: 10px;
        border: 1px solid $border_c0lor0;
     }

    /* BREAKDOWN: f(flow) - Product(Name of the Overall idea)
     * fm-tweet: initial parent (parent)
     ************************************************************************ */
    .fm-products-tweets{
        padding: 20px 10px;
        width: 66%;
        background: $brand_color;
    
        /* Denoted with "_" to show it is a child of the "tweet" parent
         * _tweet-box0: direct decendant of parent (child)
         ******************************************************************** */
        & ._tweet-box0{
            border: 1px solid $border_radius01;
            padding: 6px;
            box-sizing: border-box;
        }
        
        /* Denoted with a "__" to show that is it nested of "box" 
         * __box0-title: parent's direct decendant's child (grandchild)
         ******************************************************************** */      
        & .__box0-title{
            color: $text_color01;
            font-size: $text_size01;
            
        }
    }

```
#### 5. HTML Preview of LOC
If you notice, inside of an HTML document you should be able to trace back to the parent, and know where the CSS group is written.

```markup
    <!-- Global Reusable Box Layout Component -->
    <div class="g-box01">
    
        <!-- Product Owns the contents below, and is shown through naming -->
        <div class="f-products">
            <div class="fm-products-tweets">
                <div class="_tweet-box0">
                    <div class="__box0-title">Hello World!</div>
                    
                    <!-- When declaring different flows inside of nested groups, one has to redeclare the owner level of the component -->
                    <button class="g-btn _btn-md">Submit</button>
                </div>
                <div class="_tweet-box0">
                    <div class="__box0-title">Hello World!</div>
                    
                    <!-- When declaring different flows inside of nested groups, one has to redeclare the owner level of the component -->
                    <button class="g-btn _btn-md">Submit</button>
                </div>
            </div>
        </div>
    </div>
```

#### 6. CSS Partial's File Structure
Coming Soon..