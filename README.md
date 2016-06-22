# Barebones Vue Components

This is a collection of Vue.js components I've used in a number of projects, stripped of the project-specific markup to make them flexible, easy to use and customize in any project.

## Components

### Mailchimp List Subscription
An email input form that sends a request to add a subscriber to a Mailchimp list and responds with either a success or error message.

Usage: 
`<mailchimp-subscribe action='{ String: Mailchimp Form Action }'></mailchimp-subscribe>`

### Product Image Gallery
A simple component that displays a single large image with a list of clickable thumbnails – typically used for product detail pages.

Usage:
`<product-image-gallery :images='{ Array: Product Images }'></product-image-gallery>`