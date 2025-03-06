
# Component Storybook Documentation Template

```
Task : Create Storybook template for the component <componentName>

## 1. File Structure

components/{component-name}/
├── stories/
│ ├── __WIP__{ComponentName}_Overview-story.mdx
│ ├── __WIP__{ComponentName}_Recipes-story.mdx
│ ├── __WIP__{ComponentName}_Playground-story.tsx
│ └── __WIP__{ComponentName}_RegressionTesting-story.tsx


## 2. Story Structure

### Overview Story (ComponentName_Overview-story.mdx)
- Component introduction and links (Github, Figma, Jira)
- Guidelines and best practices
- Basic component API demonstration
- Props documentation (ArgsTable)
- Default implementation example

### Recipes Story (ComponentName_Recipes-story.mdx)
- Common use cases and patterns
- Each recipe should include:
  - Description of the use case
  - Code example
  - Visual demonstration
  - Relevant props configuration
- Cover variations like:
  - Basic usage
  - With different prop combinations
  - Common state variations
  - Special cases

### Playground Story (ComponentName_Playground-story.tsx)
- Interactive demo with adjustable props
- Default configuration
- All available props exposed for testing
- Clean, minimal implementation

### Regression Testing Story (ComponentName_RegressionTesting-story.tsx)
- Comprehensive prop combinations
- Edge cases
- Visual regression scenarios
- Accessibility testing scenarios

## 3. Documentation Guidelines

### Component Description

# {ComponentName}


[Github](link) | [Figma](link) | [Jira](link)

Brief description of the component's purpose and main features.


## Guidelines
<keep it empty> like this [guidelines]


### Code Examples
typescript
// Basic implementation
export const Basic = (args) => {
return <Component {...args} />;
};
// Story configuration
export default {
title: 'Category/ComponentName',
component: Component,
parameters: {
viewMode: 'docs',
previewTabs: {
canvas: { hidden: true }
},
percy: { skip: true }
}
};



## 4. Props Documentation

use ArgsTable to create prop table


## 5. Story Organization
- Group related stories together
- Use consistent naming conventions
- Provide clear descriptions
- Include visual examples
```
