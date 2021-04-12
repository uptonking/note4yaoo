---
title: lib-ui-spectrum-docs-components
tags: [adobe-spectrum, components, docs]
created: '2021-04-12T17:59:32.301Z'
modified: '2021-04-12T18:07:34.356Z'
---

# lib-ui-spectrum-docs-components

> - platform-specific; - theme-specific; 

# [overview](https://react-spectrum.adobe.com/react-spectrum/getting-started.html)

- It provides components that are adaptive to interactions and screen sizes across devices, and includes full screen reader and keyboard navigation support for accessibility.

- All React Spectrum applications start with a `Provider`. 
  - The `Provider` specifies the theme to use, along with application level settings like the locale. 
  - Inside the `Provider`, you should render your application, including all React Spectrum components.
  - You must ensure that the version of the `Provider` component and the `theme` that you use is greater than or equal to the newest version of any component in your app.

# Provider

- Provider is the container for all React Spectrum applications. 
  - It defines the theme, locale, and other application level settings, and can also be used to provide common properties to a group of components.
