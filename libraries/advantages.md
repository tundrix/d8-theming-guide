## The advantages of libraries and dependencies

Copied from the issue summary of [2377397](https://www.drupal.org/node/2377397):

1. dependencies, hence a step towards getting rid of weights
2. one uniformly applied system for modules and themes alike
3. themes are also forced to think about categorisation in their CSS
4. libraries can contain CSS and JS as logically associated units, and can declare dependencies on other libraries
5. themes are encouraged to create a library per component/topic/logical unit and hence are encouraged to not load all their CSS on all pages anymore, but to attach it when appropriate in a preprocess hook and/or only on the relevant pages via hook_page_attachments_alter()
