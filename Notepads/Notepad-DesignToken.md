# Notepad-DesignToken

## Identification Rules

1. ONLY identify values for:

   - margin
   - padding
   - gap
   - positioning properties (top, right, bottom, left)

2. DO NOT change:

   - width/height
   - dimensional properties
   - values < 2px
   - border radius
   - negative values
   - non-spacing properties

3. Available tokens: $2 through $128 (see spacers.ts)
   spacers = {
   $2: '2px',
   $4: '4px',
   $8: '8px',
   $12: '12px',
   $16: '16px',
   $20: '20px',
   $24: '24px',
   $32: '32px',
   $40: '40px',
   $48: '48px',
   $64: '64px',
   $72: '72px',
   $128: '128px'
   }
4. ONLY replace values that EXACTLY match a token in the spacers list:
   Valid replacements: 2px, 4px, 8px, 12px, 16px, 20px, 24px, 32px, 40px, 48px, 64px, 72px, 128px
   Do NOT replace any value that doesn't exactly match a token (e.g., 14px, 6px, 10px, etc.)
   Values must be an EXACT match:
   16px can be replaced with ${spacers.$16}
   14px should remain as 14px (do NOT approximate to closest token)
   Never round values up or down to fit a token

## Application Steps

1. Import Check:
   // Add if missing at the top of file:
   import { spacers } from '@zocdoc-mezzanine/foundations-layout

2. Direct Value Replacement:

   - Find: `property: Xpx;`
   - Replace: `property: ${spacers.$X};`
     Example:

   ```typescript
   // Before: padding: 16px;
   // After:  padding: ${spacers.$16};
   ```

3. Compound Values:

   - Find: `property: Xpx Ypx;`
   - Replace: `property: ${spacers.$X} ${spacers.$Y};`
     Example:

   ```typescript
   // Before: padding: 12px 16px;
   // After:  padding: ${spacers.$12} ${spacers.$16};
   ```

4. Variable Declarations:

   - Find: `const NAME = Xpx;`
   - Replace: `const NAME = spacers.$X;`
     Example:

   ```typescript
   // Before: const ICON_MARGIN = 8;
   // After:  const ICON_MARGIN = spacers.$8;
   ```

5. Template Literal Updates:

   - Find: `${value}px`
   - Replace: `${spacers.$value}`
     Example:

   ```typescript
   // Before: gap: ${ICON_MARGIN}px
   // After:  gap: ${spacers.$8}
   ```

6. Math Operations:
   When tokens are used in calculations:
   ```typescript
   // Before: padding: (8 + 4)px;
   // After:  padding: calc(${spacers.$8} + ${spacers.$4});
   ```

## Validation Steps

1. Check imports are correct
2. Verify no dimensional properties were changed
3. Confirm negative values remain unchanged
4. Test component renders correctly
5. Verify spacing matches original design

## Common Patterns

1. Direct replacements:

   ```typescript
   margin: 16px;        → margin: ${spacers.$16};
   padding: 8px 16px;   → padding: ${spacers.$8} ${spacers.$16};
   gap: 8px;           → gap: ${spacers.$8};
   ```

2. Keep as-is:
   ```typescript
   width: 16px;        // dimensional - keep
   margin: -1px;       // negative - keep
   border-radius: 2px; // border radius - keep
   ```

## Testing

1. Visual regression testing
2. Component spacing verification
3. Responsive layout checks
