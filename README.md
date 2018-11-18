# WordPress Project README Template
## Overview

A few sentences to a paragraph about what the site is. Examples:

* A brochure site with little user interactive functionality, but complex design templates.
* A complex site for a product manufacturer with a number of custom post types and taxonomies to organize product information.
* A site with a small public face, and a very deep private members-only area.

## Running the Project

* `git clone` the repository somewhere that PHP, Apache, and MySQL can run (WordPress needs those).
* `npm install` to install the necessary packages.
* `gulp` or `gulp watch` to start compiling the assets.
* Get the WordPress database (or don't in some cases: sometimes it doesn't matter if you have all the up-to-date content).
* Run the standard WordPress installer.
* Get login information and other private stuff ffrom the [intranet page/password safe/etc](#!).

### Gotchas

* Some JavaScript is in `src/js/` but some is also in `wp-content/themes/themename` because we had trouble with our build tools and some JS. If you can fix it and get all our JS working in the build tools again, feel free!
* Some developers have had trouble running the project in certain local environments. Deleting and regenerating the `.htaccess` file seems to fix it for the most part. Be sure to save our custom config in the `.htaccess`.

## Plugins
A list of all active plugins on the site.

| Name  | Function/Description | :warning: Warnings
| --- | --- | --- |
| Advanced Custom Fields | Provides most of the custom functionality on site. | Don't deactivate. |
| Gravity Forms | Create dozens of forms on the site. | Don't deactivate. |
| Breadcrumb NavXT | Create breadcrumbs on the site. | n/a |

## Custom Templates
| Name | Filename | Function/Description | :warning: Warnings
| --- | --- | --- | --- |
| Homepage | `page-home.php` | -- | :x: Don't re-use. |
| Locations | `page-locations.php` | Custom template. Loops through ACF Repeater location data that activates when this template is applied to a page. | :x: Don't re-use. |
| Sectioned | `page-sectioned.php` | Custom template. Loops through ACF Repeater location data that activates when this template is applied to a page. | :heavy_check_mark: Re-use. | 

## Custom Post Types
A list of all actively used custom post types on the site.

| Label/Name  | $post_type | Description | Archive? | Single? |
| --- | --- | --- | --- | --- |
| Staff  | `ds_staff` | The staff members of DSI. Heavy customization with ACF. | Yes | Yes |
| Services | `ds_services`  | The services of DSI. Light customization with ACF, but complex taxonomies. | No | Yes | 
| Brochures | `ds_brochures`  | Brochures for services of DSI. No templates -- single redirects to the PDF attachment for the post. Archive is not used. Brochures are presented on Services pages using shortcodes or template functions. | No | No | 

## Custom Taxonomies
A list of all actively used custom taxonomies on the site.

| Label/Name | $taxonomy | Description | Example of Term | Post Type
| --- | --- | --- | --- | --- |
| Staff Type | `ds_staff_type` | Used to categorize staff members by department. | C-levels, Developers, Marketers | Staff |
| Service Areas | `ds_service_area`  | Used to categorize services by various regions, states, and locales serviced. | New Jersey, Northeast, USA | Services |
| Service Certifications | `ds_service_certification`  | Used to add various certifications to services. | Awesome Certification, Great Certification | Services |
| Service Market | `ds_service_market`  | Used to categorize services by their expected market demographic. | B2B, B2C | Services |

## Custom Functionality
| Name | Filename | Function/Description | :warning: Warnings
| --- | --- | --- | --- |
| Vcard Generator | `mu-plugins/inc/generate-vcard.php` | Generate vcards from ACF data on the Staff post type. | Generated vcards aren't added to the repo. There's a function in the vcard file that will run every ~hour and automatically regenerate them for you. |
| Content Locker | `mu-plugins/inc/content-locker.php` | Lock content behind a Gravity Forms form submission wall. Also sends the information to the correct Mailchimp and Marketo lists. | n/a |

## Issues Log :warning:
| Name | Date | Description | 
| --- | --- | --- | 
| Slow page | ~Apr 2017 | We discovered there were over 10,000 items in the taxonomy. The plugin we're using unfortunately has scalability issues and cannot handle this many items in the taxonomy. The client agreed to keep the taxonomy below 2,000 items. |
| New content types | Oct 2018 | After the 3.5.0 update on Big Plugin, we found that Other Plugin was failing to add new post types. The workaround/fix is visiting Specific Page in the admin panel, and manually regenerating Other Plugin's post types. |