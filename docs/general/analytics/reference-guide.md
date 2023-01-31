---
layout: default
title: Reference Guide
parent: Analytics
grand_parent: General
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

### Master Tag (SS-MT)
The Search Station Master Tag contains all the events tracked on brochure websites by Search Station across board. It is to be updated as new events of interests come up. 

### WooCommerce Master Tag (SS-WC-MT)
The Search Station WooCommerce Master Tag contains all the events tracked on e-commerce (WooCommerce) websites by Search Station across board. It is to be updated as new events of interests come up. It contains woocommerce events and all the events in the Search Station Master Tag.

### Tracked Sites
A list of sites that have been set up in line with the Search Station Tracking System are as follows; 

| No. | Website       | Domain                                                                        | Type       | Tag       | Brand |
|:----|:--------------|:------------------------------------------------------------------------------|:-----------|:----------|:------|
|  1  | CIS           | [contractinteriorsystems.co.uk](https://www.contractinteriorsystems.co.uk/)   | Brochure   | SS-MT     |  WIC  |
|  2  | CTX           | [ceilingtilesexpress.co.uk](https://ceilingtilesexpress.co.uk/)               | E-Commerce | SS-WC-MT  |  WIC  |
|  3  | WIS           | [workplaceinteriorshop.co.uk](https://workplaceinteriorshop.co.uk/)           | E-Commerce | SS-WC-MT  |  WIC  |
|  4  | Gravity       | [gravityofficeinteriors.co.uk](https://www.gravityofficeinteriors.co.uk/)     | Brochure   | SS-MT     |  WIC  |
|  5  | GPUK          | [glasspartitioninguk.co.uk](https://www.glasspartitioninguk.co.uk/)           | Brochure   | SS-MT     |  WIC  |
|  6  | Ruya          | [ruyarecruitment.com](https://ruyarecruitment.com/)                           | Brochure   | SS-MT     |  WIC  |
|  7  | Lake & Co.    | [lakecoflooring.co.uk](https://lakecoflooring.co.uk/)                         | Brochure   | SS-MT     |  WIC  |
|  8  | LineMark      | [line-mark.com](https://www.line-mark.com/)                                   | Brochure   | SS-MT     |  SS   |


| No. | Website       | Domain                                                                        |
|:----|:--------------|:------------------------------------------------------------------------------|
|  1  | CIS           | [contractinteriorsystems.co.uk](https://www.contractinteriorsystems.co.uk/)   |
|  2  | CTX           | [ceilingtilesexpress.co.uk](https://ceilingtilesexpress.co.uk/)               |
|  3  | WIS           | [workplaceinteriorshop.co.uk](https://workplaceinteriorshop.co.uk/)           |
|  4  | Gravity       | [gravityofficeinteriors.co.uk](https://www.gravityofficeinteriors.co.uk/)     |
|  5  | GPUK          | [glasspartitioninguk.co.uk](https://www.glasspartitioninguk.co.uk/)           |
|  6  | Ruya          | [ruyarecruitment.com](https://ruyarecruitment.com/)                           |
|  7  | Lake & Co.    | [lakecoflooring.co.uk](https://lakecoflooring.co.uk/)                         |
|  8  | LineMark      | [line-mark.com](https://www.line-mark.com/)                                   |


| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |


### Tracked Events
Events tracked by the Search Station Tracking System are;
| No. | event                 | parameter1(`parameter_value`), parameter2(`'String Value'`),...            | Push Method |
|:----|:----------------------|:---------------------------------------------------------------------------|:------------|
|  1  | generate_lead         | form_title(`variable`), form_entry(`variable`)                             | PHP         |
|  2  | postcode_lookup       | postcode_value(`variable`), postcode_status(`'String'`)                    | JavaScript  |
|  3  | calendly              | calendly_action(`'string_value'`)                                          | JavaScript  |

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