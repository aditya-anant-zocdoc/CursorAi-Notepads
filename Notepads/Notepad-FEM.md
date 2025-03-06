# Notepad FEM implementation

```
Task

Implement metrics tracking for a React component using existing patterns and utilities.

Context

The objective is to integrate metrics tracking into a React component while ensuring consistency with established best practices.

Requirements

1. COMPONENT METRICS PATTERN:
  1. Create/update three files:(if not already present)
    - Base{Component}.tsx - Core component without metrics
    - Metrics{Component}.tsx - Wrapper that adds metrics functionality
    - {Component}.tsx - Main export using Metrics{Component}

  2. MetricsComponent should:
    - Import useCustomMetrics(if custom click/change event requried) and MezzMetrics
    - Forward ref from main component
    - Handle all metrics-related logic
    - Wrap BaseComponent with MezzMetrics

  3. Main component should:
    - Import and use MetricsComponent
    - Handle prop types and exports
    - Not contain direct metrics logic


2. Metrics Properties (for Metrics wrapper)
•	Accept standard V2MetricsProps.
•	Track key user interactions within the component.

Implementation Pattern (TypeScript)
•	Refer to @RadioTypes.ts for type-specific details.
•	Refer to  @PrimaryRadioButton.tsx and @PrimaryRadioGroup.tsx and its component for implementation details.
* Update main component with metrics type for props
* Use filterV2MetricsProps from @zocdoc-mezzanine/internal-shared to filter metrics props and than pass it down to metrics wrapper

// ❌ INCORRECT - ref going to inner component
<MezzMetrics {...props}>
    <Component ref={ref} />
</MezzMetrics>

// ✅ CORRECT - ref going to MezzMetrics
<MezzMetrics ref={ref} {...props}>
    <Component />
</MezzMetrics>

// ❌ INCORRECT - don't add MetricsType to component file
type ErrorMessageV2MetricsProps = Omit<V2MetricsCapturingSchema, 'v2TargetType' | 'v2TargetTrigger'>;

// ✅ CORRECT - include MetricsType in component's type file

export type <component>V2MetricsProps = Omit<V2MetricsCapturingSchema, 'v2TargetType' | 'v2TargetTrigger'>;

Testing Requirements
•	Test metric sending on key interactions.
•	Verify that metrics are only sent when v2TargetName is provided.
•	Ensure that the correct metric properties are passed.
•	Mock useCustomMetrics for testing, if required.
•	Refer to @PrimaryRadioButton-tests.tsx for guidance on testing metrics.
. Use expectV2MetricWasSentWith from renderComponent to assert on metrics are send or not.
. Asser for no metrics prop are passed - 
        expect(expectV2MetricWasSentWith).toThrow(
            expect.stringMatching('sendMetric was not called')
        );

Note integrate Metrics tests in the component  test file, don’t add a new test file

Additional Notes
•	Follow best practices by separating base component logic from metrics logic.
•	Use forwardRef to maintain ref forwarding through the metrics wrapper.
•	Ensure all metric event names follow established conventions.
•	Document all metric events in the component documentation.
```
