# Web-platform Test Coverage

```
Test Coverage Rules:

1. Default Rendering
- Initial render without props
- Default prop values verification
- Server Component hydration
- Layout structure validation

2. Prop Validation
- Required props testing
- Optional props behavior
- Type constraints verification
- Prop update triggers
- Callback function testing

3. Accessibility Compliance
- ARIA attributes
- Keyboard navigation
- Focus management
- Screen reader compatibility

4. User Interactions
- Click events
- Form submissions
- Keyboard events
- Hover states
- Touch interactions

5. Error State Handling
- Error boundaries
- Error messages
- Recovery flows
- Error prop handling
- Error state UI

6. Metrics Integration
- Analytics events
- Performance metrics
- Core Web Vitals
- Loading states
- Tracking props

7. Ref Forwarding
- Ref attachment
- Ref updates
- Ref methods
- Ref cleanup
- Imperative handle

8. Edge Cases
- Empty states
- Loading states
- Boundary conditions
- Overflow handling
- Extreme prop valuesTest Coverage Rules:
[Previous rules remain the same...]



9. ARIA and Accessibility Props
- ariaLabel validation
- ariaLabelledby validation
- ariaDescribedBy validation
- role attribute testing
- tabIndex behavior and values
- aria-checked states
- aria-disabled states

10. Keyboard Navigation Testing
- Arrow key navigation (Up/Down/Left/Right)
- Space/Enter key selection
- Tab key focus management
- Shift+Tab backwards navigation
- Key combinations (if applicable)

11. Screen Reader Compatibility
- Icon + label text combinations
- Hidden helper text
- Announcement order
- State changes announcements
- Dynamic content updates

12. User Event Testing Best Practices
- Always setup userEvent at describe block level: `const user = userEvent.setup()`
- Never mix fireEvent with userEvent in the same test suite
- Remember userEvent methods are async and require `await`
- Focus management is required before keyboard events:
  - Use `await user.tab()` before keyboard interactions
  - Keyboard events only work on focused elements
  - Tab order should match expected user behavior

13. Disabled State Testing
- Don't attempt interactions on disabled elements with userEvent
- Focus on verifying disabled attributes and states:
  - `expect(element).toBeDisabled()`
  - `expect(element).toHaveAttribute('aria-disabled', 'true')`
- Test that disabled elements prevent interactions implicitly
- Verify visual indicators of disabled state

14. Test Structure Improvements
- Group related tests logically (keyboard, mouse, disabled states)
- Use descriptive test names that follow Given-When-Then
- Keep test setup DRY by using shared configurations
- Clear separation between setup, action, and assertion phases
- Reset mocks and cleanup after each test

15. Common Pitfalls to Avoid
- Don't test disabled elements with direct events
- Don't skip focus management when testing keyboard interactions
- Don't mix old (fireEvent) and new (userEvent) testing approaches
- Don't assume keyboard events work without proper focus
- Don't test implementation details of disabled state

16. Testing Library Best Practices
- Prefer userEvent over fireEvent for more realistic user interactions
- Remember userEvent better simulates actual browser behavior
- Account for async nature of userEvent operations
- Consider real browser constraints (focus, disabled states)
- Test components as users would interact with them

Test File Structure Updates:
ComponentName/
  - ComponentName.test.tsx
  - ComponentName.accessibility.test.tsx  // Separate file for extensive a11y tests

Testing Best Practices Additions:
- Use renderComponent from @zocdoc-frontend-common/test-utils
- refactor if not, to use single render function for all test. Pass props to the render function 
- use `dataTest` from renderComponent to assert element
- Follow Given-When-Then pattern
- Mock external dependencies
- Use React Testing Library user-event
- Avoid testing implementation details
- Focus on component behavior
- Include integration tests
- Proper test cleanup
- Test all boolean props in both true/false states
- Verify default prop values explicitly
- Test index-based functionality thoroughly
- Test all keyboard navigation patterns(if required)
- Verify ARIA attribute changes on state updates
- Include screen reader testing scenarios

Accessibility Coverage:
- 100% coverage of ARIA attributes
- 100% coverage of keyboard interactions
- 100% coverage of focus management
- 100% coverage of screen reader announcements


```
