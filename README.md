# Lasso-Drupal-Integration
Integration with Drupal 7 and Lasso Register API

Final Alpha:

Only SPI URL is stored within Drupal. Webform field IDs are stored directly in the code.

The module is using cURL, but there is a choice of using hook_submit(), which I abandoned for no particular reason than I found references to cURL in Lasso's documentation.

The module is working without the API header token, which needs to be removed from code.

To Do:

Identify form fields from within Drupal
- not sure how to UI this... should it be that I select from a list of possible acceptable values or enter them manuilly. Also have to make sure that a value is unique when used?

Store IDs in Drupal
- also not sure how to do this... should they be stored on a form by form basis or can one or more be global? Should this be done by ayyaching an instance in configuration from the form, or at the form level?

