# Refined Prompt for Integrating v2 Metrics into Mezzanine Components

## Task Description
Integrate v2 metrics into a Mezzanine component following established patterns from Button, Checkbox, and TextField components.

## Implementation Steps

1. **Create Metrics Wrapper Component**
   - Create `Metrics[Component].tsx` in the `private` folder
   - Implement forwardRef component wrapping the Base component with MezzMetrics
   - Set appropriate v2TargetType and v2TargetTrigger values

2. **Define Metrics Props Type**
   - Add `[Component]V2MetricsProps` type in the types file
   - Omit 'v2TargetType' and 'v2TargetTrigger' from V2MetricsCapturingSchema

3. **Update Main Component**
   - Use filterV2MetricsProps to extract metrics props
   - Pass metrics props to the wrapper component
   - For interactive components, implement appropriate event handlers

4. **Add Tests**
   - Test that metrics are sent with correct parameters
   - Test that metrics are not sent when v2TargetName is not provided
   - Test forwarding refs to the underlying element

5. **Update Documentation**
   - Add metrics documentation to README.mdx
   - Include example with v2TargetName and other metrics props

## Common Metrics Patterns

### For Non-Interactive Components (View Only)
```tsx
// MetricsComponent.tsx
export const MetricsComponent = forwardRef((props, ref) => {
  const { v2MetricsProps, ...componentProps } = props;

  return (
    <MezzMetrics
      ref={ref}
      v2TargetType="Component"
      v2TargetTrigger="View"
      {...v2MetricsProps}
    >
      <BaseComponent {...componentProps} />
    </MezzMetrics>
  );
});
```

### For Interactive Components (View + Events)
```tsx
// MetricsComponent.tsx
export const MetricsComponent = forwardRef((props, ref) => {
  const { v2MetricsProps, onChange, ...componentProps } = props;

  const handleEventMetric = useOnChangeMetrics(
    'Component', 'EventType', v2MetricsProps
  );

  const handleChange = useCallback((e) => {
    handleEventMetric();
    onChange?.(e);
  }, [onChange, handleEventMetric]);

  return (
    <MezzMetrics
      ref={ref}
      v2TargetType="Component"
      v2TargetTrigger="View"
      {...v2MetricsProps}
    >
      <BaseComponent {...componentProps} onChange={handleChange} />
    </MezzMetrics>
  );
});
```

## Test Examples
```tsx
it('should send view metric when component is rendered', () => {
  const { expectV2MetricWasSentWith } = renderComponent(
    <Component v2TargetName="Test_Component" />
  );

  expectV2MetricWasSentWith({
    target_name: 'Test_Component',
    target_type: 'Component',
    target_trigger: 'View',
    event_name: 'Component Viewed',
  });
});

it('should not send metrics when v2TargetName is not provided', () => {
  const { expectV2MetricWasSentWith } = renderComponent(
    <Component />
  );

  expect(() => expectV2MetricWasSentWith({
    target_type: 'Component',
  })).toThrow(expect.stringMatching('sendMetric was not called'));
});
```

## Required Dependencies
- @zocdoc-frontend-common/utils-frontend-metrics
- @zocdoc-mezzanine/internal-shared

## Notes
- Always filter v2 metrics props using filterV2MetricsProps utility
- Metrics are only sent when v2TargetName is provided
- For interactive components, use appropriate hooks from internal-shared
- Follow existing test patterns to verify metrics are sent correctly

## Common Issues and Solutions

### Ref Forwarding
- **Ensure ALL components in the hierarchy use forwardRef**: The Base component (e.g., BaseTag, BaseButton) must use forwardRef, not just the Metrics wrapper
- If you see errors like "Function components cannot be given refs" or metrics not being sent, check that refs are properly forwarded through the entire component tree
- When testing with additional properties (v2AdditionalProperties), specify v2TargetName directly rather than using spread operator with other props to avoid potential overrides

```tsx
// Correct implementation of BaseComponent with forwardRef
const BaseComponent = forwardRef<HTMLDivElement, BaseComponentProps>((
  { text, className, dataTest, ...props },
  ref
) => {
  return (
    <div
      ref={ref}
      className={className}
      data-test={dataTest}
    >
      {text}
    </div>
  );
});
```
