# UI Guidelines

## Design System

### Component Library
- **Framework**: Material-UI (MUI) v5 or later
- All UI components should use Material Design components from the MUI library
- Custom components should follow Material Design principles and guidelines
- Maintain consistency with Material Design's interaction patterns and visual hierarchy

## Color Palette

### Primary Colors
- **Primary**: `#1976d2` (Blue 700)
- **Primary Light**: `#42a5f5` (Blue 400)
- **Primary Dark**: `#1565c0` (Blue 800)

### Secondary Colors
- **Secondary**: `#9c27b0` (Purple 500)
- **Secondary Light**: `#ba68c8` (Purple 300)
- **Secondary Dark**: `#7b1fa2` (Purple 700)

### Status Colors
- **Success**: `#2e7d32` (Green 800)
- **Warning**: `#ed6c02` (Orange 700)
- **Error**: `#d32f2f` (Red 700)
- **Info**: `#0288d1` (Light Blue 700)

### Neutral Colors
- **Background**: `#ffffff` (White)
- **Surface**: `#f5f5f5` (Grey 100)
- **Text Primary**: `#212121` (Grey 900)
- **Text Secondary**: `#757575` (Grey 600)
- **Divider**: `#e0e0e0` (Grey 300)

### Task-Specific Colors
- **Overdue**: `#d32f2f` (Red 700)
- **Due Soon**: `#f57c00` (Orange 700)
- **Completed**: `#4caf50` (Green 500)
- **High Priority**: `#e53935` (Red 600)
- **Medium Priority**: `#fb8c00` (Orange 600)
- **Low Priority**: `#43a047` (Green 600)

## Typography

### Font Family
- **Primary Font**: 'Roboto', sans-serif
- **Monospace Font**: 'Roboto Mono', monospace (for code or technical content)

### Type Scale
- **H1**: 2.5rem (40px), font-weight: 300
- **H2**: 2rem (32px), font-weight: 400
- **H3**: 1.75rem (28px), font-weight: 400
- **H4**: 1.5rem (24px), font-weight: 400
- **H5**: 1.25rem (20px), font-weight: 500
- **H6**: 1rem (16px), font-weight: 500
- **Body 1**: 1rem (16px), font-weight: 400 (default body text)
- **Body 2**: 0.875rem (14px), font-weight: 400 (secondary text)
- **Button**: 0.875rem (14px), font-weight: 500, text-transform: uppercase
- **Caption**: 0.75rem (12px), font-weight: 400

## Button Styles

### Primary Buttons
- **Style**: Contained
- **Color**: Primary color
- **Use Case**: Main actions (e.g., "Add Task", "Save")
- **Hover State**: Slight darkening of background color
- **Disabled State**: Grey with 0.38 opacity

### Secondary Buttons
- **Style**: Outlined
- **Color**: Primary color
- **Use Case**: Secondary actions (e.g., "Cancel", "Clear Filters")
- **Hover State**: Light background with primary color tint

### Tertiary Buttons
- **Style**: Text
- **Color**: Primary color
- **Use Case**: Low-emphasis actions (e.g., "Learn More", "Skip")

### Icon Buttons
- **Style**: Icon only with ripple effect
- **Size**: 40x40px touch target minimum
- **Use Case**: Compact actions (e.g., delete, edit, favorite)

### Floating Action Button (FAB)
- **Use Case**: Primary action on mobile views (e.g., "Add Task")
- **Position**: Bottom-right corner, 16px margin
- **Color**: Primary or Secondary color

## Spacing and Layout

### Grid System
- **Breakpoints**:
  - xs: 0px (mobile)
  - sm: 600px (tablet)
  - md: 960px (small laptop)
  - lg: 1280px (desktop)
  - xl: 1920px (large desktop)

### Spacing Scale (8px base unit)
- **xs**: 4px (0.5 unit)
- **sm**: 8px (1 unit)
- **md**: 16px (2 units)
- **lg**: 24px (3 units)
- **xl**: 32px (4 units)
- **xxl**: 48px (6 units)

### Container
- **Max Width**: 1200px for main content
- **Padding**: 24px on desktop, 16px on mobile

## Accessibility (WCAG 2.2 Level AA)

### Color Contrast
- **Normal Text**: Minimum contrast ratio of 4.5:1
- **Large Text** (18pt+ or 14pt+ bold): Minimum contrast ratio of 3:1
- **UI Components**: Minimum contrast ratio of 3:1 against adjacent colors
- Never rely on color alone to convey information

### Keyboard Navigation
- All interactive elements must be keyboard accessible
- Focus indicators must be clearly visible with minimum 3:1 contrast ratio
- Logical tab order following visual flow
- Support standard keyboard shortcuts (Enter, Space, Escape, Arrow keys)

### Screen Reader Support
- Use semantic HTML elements (button, nav, main, etc.)
- Provide descriptive ARIA labels for all interactive elements
- Use `aria-live` regions for dynamic content updates
- Ensure proper heading hierarchy (H1 → H2 → H3, etc.)
- Add alt text for all meaningful images

### Form Accessibility
- Label all form inputs with visible labels
- Provide clear error messages with `aria-describedby`
- Use `aria-invalid` for fields with errors
- Group related inputs with fieldset and legend
- Ensure minimum touch target size of 44x44px on mobile

### Motion and Animation
- Respect `prefers-reduced-motion` media query
- Provide option to disable animations
- Keep animations under 200ms for micro-interactions
- Avoid flashing content (max 3 flashes per second)

### Focus Management
- Manage focus for modals and dialogs
- Return focus to trigger element when closing modals
- Provide skip navigation links for repetitive content
- Ensure focus is never trapped unintentionally

## Responsive Design

### Mobile-First Approach
- Design for mobile screens first, then scale up
- Use responsive breakpoints for different device sizes
- Ensure touch targets are minimum 44x44px
- Optimize for one-handed use on mobile devices

### Adaptive Components
- Navigation: Drawer on mobile, persistent sidebar on desktop
- Task list: Single column on mobile, multi-column on desktop
- Forms: Stack inputs on mobile, side-by-side on desktop
- Buttons: Full-width on mobile when appropriate

## Iconography

### Icon Library
- Use Material Icons or Material Symbols
- **Icon Sizes**: 16px, 20px, 24px (default), 32px, 48px
- Ensure icons have semantic meaning and include text labels or tooltips

### Common Icons
- Add: `add_circle`, `add`
- Edit: `edit`, `edit_note`
- Delete: `delete`, `delete_outline`
- Complete: `check_circle`, `done`
- Due Date: `event`, `schedule`
- Priority: `flag`, `priority_high`
- Filter: `filter_list`
- Sort: `sort`
- Search: `search`

## Component-Specific Guidelines

### Task Cards
- Use `Card` component with elevation of 1
- Hover state: Increase elevation to 4
- Include checkbox for completion status
- Display priority indicator as colored left border (4px width)
- Show due date with calendar icon and relative time
- Actions (edit, delete) appear on hover or always visible on mobile

### Task Input Form
- Use `TextField` with outlined variant
- Provide real-time validation feedback
- Use `DateTimePicker` for due date selection
- Include `Select` or `ButtonGroup` for priority selection
- Show character count for task description

### Modals and Dialogs
- Use `Dialog` component
- Include clear title with `DialogTitle`
- Provide actions in `DialogActions` (Cancel, Confirm)
- Ensure escape key closes dialog
- Trap focus within dialog when open

### Empty States
- Display friendly illustrations or icons
- Include helpful message and call-to-action
- Use Typography variant "body1" for messages
- Center content vertically and horizontally

## Dark Mode Support

### Implementation
- Support system preference detection
- Provide manual toggle for user override
- Store preference in local storage

### Dark Mode Colors
- **Background**: `#121212`
- **Surface**: `#1e1e1e`
- **Primary**: `#90caf9` (Blue 200)
- **Text Primary**: `#ffffff`
- **Text Secondary**: `#b0b0b0`

### Dark Mode Considerations
- Adjust elevation with lighter surface colors
- Ensure minimum contrast ratios are maintained
- Use slightly desaturated colors to reduce eye strain
