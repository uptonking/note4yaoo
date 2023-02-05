---
title: lib-ui-spectrum-docs
tags: [adobe-spectrum, docs]
created: 2021-04-12T16:43:48.280Z
modified: 2021-04-12T18:07:17.615Z
---

# lib-ui-spectrum-docs

# guide

# pieces

# [layout](https://react-spectrum.adobe.com/react-spectrum/layout.html)

- The `Flex` and `Grid` components are containers, which are responsible for the layout of their children. 
  - `Flex` follows the CSS flexbox algorithm, while `Grid` implements CSS grid. 
- In general, you should prefer using flex and grid over other CSS layout models.
  - Spacing between components should be left to parent layout components rather than added as via margins to specific children. 
  - This helps ensure components are composable when reused in different places, and ensures that spacing is consistent.
- some React Spectrum components include pre-built layouts which you can insert your content into via slots. 
  - This often happens automatically through the use of semantic elements, but can also be configured through props. 
  - For example, the `Dialog` component accepts `Heading/Content/Footer` elements as children and will handle the layout automatically.
- The `Flex` component can be used to create flexbox containers, and any React Spectrum component can be used as a child. 
  - React Spectrum also shims the `gap` property, along with `rowGap` and `columnGap`
- Several React Spectrum components include pre-defined layouts that you can insert elements into via slots. 

# [styling](https://react-spectrum.adobe.com/react-spectrum/styling.html)

- React Spectrum components are designed to be consistent across all Adobe applications.
  - They include built-in styling that has been considered carefully, and extensively tested. 
  - In general, customizing Spectrum design is discouraged, but most components do offer control over layout and other aspects. 
  - In addition, you can use Spectrum defined variables to ensure your application conforms to design requirements, and is adaptive across platform scales and color schemes.
- All React Spectrum components support a limited set of styling options, including layout, spacing, sizing, and positioning options. 
  - While internal component styles such as padding, colors, borders and text styles are included in Spectrum and not available to override, external styles like margins and sizes can be set on all components.
- Where applicable, each style property accepts Spectrum defined variables in addition to raw CSS values. 
  - Using Spectrum variables is preferred wherever possible.
- Sometimes, you may find yourself needing to build a component that doesn't exist in Spectrum yet.
  - In these cases, you can ensure consistency with other Spectrum components by utilizing existing Spectrum variables. 
  - These variables could be consumed in CSS directly, but if you're building something simple, you could consider using the `View` component from React Spectrum. 
  - `View` is like a `div` or `span`

- While the traditional `className` and `style` props are not supported in React Spectrum components, there are two escape hatches that you can use at your own risk. 
  - These are `UNSAFE_className` and `UNSAFE_style`. 
  - Use of these props should be considered a last resort.

# [theming](https://react-spectrum.adobe.com/react-spectrum/theming.html)

- React Spectrum is built to support theming. 
  - Colors, sizing, and spacing options can be customized through the use of CSS variables which are defined using the Provider component. 
  - Themes consist of variable definitions for light and dark color schemes, along with medium and large platform scales. 
  - Themes can also be nested to allow different parts of an application to adopt a different appearance.
- React Spectrum supports multiple color schemes within a theme, including light and dark mode.
- React Spectrum themes support multiple platform scales.

- Themes are specified by passing a `Theme` object to the `Provider` component. 
  - This object includes several css modules which define the values for the variables in each color scheme and platform scale. 
  - Each CSS module defines a CSS class which includes the variables it defines, 
  - and `Provider` applies these classes according to media queries and prop settings.
- React Spectrum includes three themes by default.
  - The defaultTheme uses the Spectrum light and darkest color themes and is suitable for most applications.
  - The darkTheme uses the Spectrum dark and darkest color themes, and is suitable for applications that are optimal with a darker interface regardless of operating system setting (e.g. photo/video editors).
  - The lightTheme uses the Spectrum lightest and darkest color themes, and is suitable for applications that require high brightness levels while in light mode and high contrast ratios while in dark mode.

# [ssr: Server Side Rendering](https://react-spectrum.adobe.com/react-spectrum/ssr.html)

- SSR is the process of rendering components to HTML on the server, rather than rendering them only on the client. 
- Static rendering is a similar approach, but pre-renders pages to HTML at build time rather than on each request. 
- These techniques can help improve perceived loading performance and SEO. 
- React Spectrum supports both of these approaches, either through a custom implementation or via frameworks like Next.js and Gatsby.
