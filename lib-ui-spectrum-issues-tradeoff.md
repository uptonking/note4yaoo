---
title: lib-ui-spectrum-issues-tradeoff
tags: [adobe-spectrum, components, issues, tradeoff]
created: 2021-05-10T13:46:31.467Z
modified: 2021-05-10T13:48:02.087Z
---

# lib-ui-spectrum-issues-tradeoff

# guide

# engineering

- ## Separate Menu and ListBox into different components
- https://github.com/adobe/react-spectrum/pull/254
- This splits Menu into two components: 
  - Menu (as used with MenuTrigger), 
  - and ListBox (used inside Picker, ComboBox, etc.). 
- The components have slightly different usecases and accessibility requirements, so this makes sense. 
- The differences between them are:
  - Menu is not virtualized using CollectionView whereas ListBox is. 
    - Menus have the requirement of automatically resizing to fit their content, which is not possible with virtualization. 
    - When used with Pickers and ComboBoxes, ListBoxes have a fixed width. 
    - In general, we expect the length of most Menus to be relatively short (e.g. a fixed list of actions), whereas Pickers and ComboBoxes may contain many items.
  - Menu uses `role=menu` with role=menuitem, role=menuitemradio, or role=menuitemcheckbox for its items whereas ListBox uses `role=listbox` with role=option for its items.
  - ListBox uses `aria-multiselectable` whereas Menu does not.
  - Menu items use `aria-checked` whereas ListBox items use `aria-selected`
  - Menus have `onClose` behavior with different enter and space key behavior.
  - According to Spectrum, Menu items can have keyboard shortcuts and other information/controls on the right side of each item, whereas ListBox items cannot.
- `useSelectableList` hook has been added that wraps `useSelectableCollection` and adds a default keyboard handler for non-virtualized lists. 
  - It uses the DOM to get layout information (e.g. for implementing page up/page down support). 
  - When non-virtualized, a `data-key` attribute is added to each item, so that DOM nodes can be found by their key.
  - In addition, keyboard navigation now skips disabled items. 
  - aria-posinset and aria-setsize have been added to items when virtualized.
