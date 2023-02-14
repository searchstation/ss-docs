---
layout: default
title: Reference Guide
parent: Analytics
grand_parent: Processes
nav_order: 4
---

# Reference Guide
{: .no_toc}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### Introduction
This Reference Guide is aimed at providing more guidance to the processes employed in creating a system around the Search Station Tracking Setup. 

### (SS-MT.json)
The Search Station Master Tag (SS-MT.json) contains all the events tracked on brochure websites by Search Station across board. It is to be updated as new events of interests come up. 

### (SS-WC-MT.json)
The Search Station WooCommerce Master Tag (SS-WC-MT.json) contains all the events tracked on e-commerce (WooCommerce) websites by Search Station across board. It is to be updated as new events of interests come up. It contains woocommerce events and all the events in the Search Station Master Tag.

### Tracked Sites
A list of sites that have been set up in line with the Search Station Tracking System are as follows; 

| Website       | Domain                                                                                                 | Type       | Tag       | Brand |
|:--------------|:-------------------------------------------------------------------------------------------------------|:-----------|:----------|:------|
| CIS           | <a href="https://www.contractinteriorsystems.co.uk/" target="_blank">contractinteriorsystems.co.uk</a> | Brochure   | SS-MT     |  WIC  |
| CTX           | <a href="https://ceilingtilesexpress.co.uk/" target="_blank">ceilingtilesexpress.co.uk</a>             | E-Commerce | SS-WC-MT  |  WIC  |
| WIS           | <a href="https://workplaceinteriorshop.co.uk/" target="_blank">workplaceinteriorshop.co.uk</a>         | E-Commerce | SS-WC-MT  |  WIC  |
| Gravity       | <a href="https://www.gravityofficeinteriors.co.uk/" target="_blank">gravityofficeinteriors.co.uk</a>   | Brochure   | SS-MT     |  WIC  |
| GPUK          | <a href="https://www.glasspartitioninguk.co.uk/" target="_blank">glasspartitioninguk.co.uk</a>         | Brochure   | SS-MT     |  WIC  |
| Ruya          | <a href="https://ruyarecruitment.com/" target="_blank">ruyarecruitment.com</a>                         | Brochure   | SS-MT     |  WIC  |
| Lake & Co.    | <a href="https://lakecoflooring.co.uk/" target="_blank">lakecoflooring.co.uk</a>                       | Brochure   | SS-MT     |  WIC  |
| LineMark      | <a href="https://www.line-mark.com/" target="_blank">line-mark.com</a>                                 | Brochure   | SS-MT     |  SS   |



### Tracked Events
Events tracked by the Search Station Tracking System are;

| event            | parameter_name(`parameter_value`)...                     | Sites Used               | Theoretical file    | Push Tech   |
|:-----------------|:---------------------------------------------------------|:-------------------------|:--------------------|:------------|
| generate_lead    | form_title(`variable`), form_entry(`variable`)           | Sites with Gravity Forms | theme-support.php   | PHP         |
| postcode_lookup  | postcode_value(`variable`), postcode_status(`'String'`)  | LineMark                 | postcode-lookup.php | JavaScript  |
| calendly         | calendly_action(`'string_value'`)                        | LineMark                 | ga-events.js        | JavaScript  |

### Code Samples
The events can be executed with the respective code snippets;
1. generate_lead
    ```php
    add_filter( 'gform_confirmation', 'gform_confirmation_push', 10, 4 );
    function gform_confirmation_push( $confirmation, $form, $entry, $ajax ) {
        if ( ! is_string( $confirmation ) ) {
            return $confirmation;
        }
        $form_title = rgar( $form, 'title' );
        $entry_id = rgar( $entry, 'id' );
        $confirmation .= GFCommon::get_inline_script_tag( "window.dataLayer.push({'event': 'generate_lead','form_title': '$form_title', 'form_entry' : ".$entry_id."});" );
        return $confirmation;
    }
    ```

2. postcode_lookup
    ```javascript
    function postcode_lookup_success(postcode) {
        postcode_response_empty()
        postcode_form.hide()
        postcode_loader.hide();
        window.dataLayer.push({'event': 'postcode_lookup','postcode_value': postcode, 'postcode_status' : 'Found'});
    }
  ```

3. calendly
    ```javascript
    jQuery(document).ready(function() {
        jQuery('#quote').on('mouseenter', function() {
        if (!jQuery(this).hasClass('hovered') ) {
            window.dataLayer.push({'event': 'calendly', 'calendly_action' : 'ss_iframe_hover'});
            jQuery(this).addClass('hovered');
        }
        })
    });
    ```