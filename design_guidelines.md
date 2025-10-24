# Design Guidelines: Sleep Monitor & Dream Journal App

## Design Approach & Philosophy

**Selected Approach:** Wellness App Reference-Based Design
Drawing inspiration from Calm, Headspace, and Sleep Cycle for their calming, data-friendly interfaces that balance utility with emotional comfort. The design prioritizes tranquility, ease of use, and gentle data visualization.

**Core Principles:**
- Soft, rounded aesthetics to promote relaxation
- Generous whitespace for breathing room and reduced cognitive load
- Smooth, subtle animations that feel organic, not mechanical
- Data visibility without overwhelming the user
- Nighttime-friendly interface considerations

---

## Typography System

**Font Selection:**
- Primary: Inter or DM Sans (via Google Fonts CDN) - excellent readability for data
- Accent: Instrument Serif or Playfair Display - for headlines and wake-up messages

**Type Scale:**
- Hero messages: text-4xl to text-5xl, font-light
- Section headings: text-2xl, font-medium
- Card titles: text-lg, font-semibold
- Body text: text-base, font-normal
- Data labels: text-sm, font-medium
- Timestamps/meta: text-xs, font-normal

**Line Heights:** Generous spacing (leading-relaxed to leading-loose) for readability

---

## Layout System

**Spacing Primitives:** Tailwind units of 3, 4, 6, 8, 12, 16
- Component padding: p-6 or p-8
- Card gaps: gap-6
- Section spacing: py-12 to py-16
- Input spacing: space-y-4

**Container Strategy:**
- Max width: max-w-7xl for main dashboard
- Cards: Full width on mobile, grid-cols-1 md:grid-cols-3 for three-card layout
- Charts section: max-w-4xl centered

**Grid Structure:**
- Three-card input layout: Equal-width cards in desktop (grid-cols-3), stacked on mobile
- Dashboard overview: 2-column split (recent logs + insights)

---

## Component Library

### 1. Navigation
**Top Bar:**
- Clean header with app logo/name (left), date indicator (center), user profile icon (right)
- Fixed position with subtle shadow or border-bottom
- Height: h-16, padding px-6

### 2. Wake-Up Message Card
**Hero Component:**
- Prominent placement at top of dashboard
- Large typography with personalized greeting
- Weather icon integration (use Heroicons for weather)
- Minimum height: min-h-[200px], rounded-3xl
- Background: Soft gradient backdrop (implementation detail, not color)
- Padding: p-8 to p-12

### 3. Three-Card Input Layout
**Card Structure:**
Each card follows identical pattern:
- Rounded corners: rounded-2xl
- Padding: p-6
- Shadow: shadow-lg with soft elevation
- Border: border with subtle opacity

**Sleep Card:**
- Time pickers for bedtime/wake time
- Quality slider (1-10 scale with emoji indicators)
- Duration auto-calculated display
- Icon: Moon from Heroicons

**Lifestyle Card:**
- Toggle switches for exercise (yes/no)
- Stepper for caffeine intake (cups)
- Stress level slider (1-5 scale)
- Icon: Activity from Heroicons

**Dream Card:**
- Large textarea: min-h-[120px], rounded-xl
- Voice recording button: Prominent circular button (w-14 h-14) with microphone icon
- Voice waveform visualization during recording
- Tag input for dream themes
- Icon: Cloud from Heroicons

### 4. Voice Recording Interface
**Recording State:**
- Pulsing animation on microphone button during active recording
- Timer display: text-lg, font-mono for clarity
- Waveform visualization: 30-40 vertical bars with animated heights
- Stop/Cancel buttons below waveform
- Transcript preview area after recording completion

### 5. Sleep Log History
**List View:**
- Chronological cards with most recent first
- Each entry: rounded-xl, p-4, mb-3
- Compact layout showing: date, duration, quality indicator, weather icon
- Expandable to show full details and dream entry
- Delete/edit icons (small, top-right of each card)

### 6. Charts & Insights Section
**Chart Container:**
- Full-width section with heading "Your Sleep Patterns"
- Two-column grid on desktop: grid-cols-1 lg:grid-cols-2
- Each chart card: rounded-2xl, p-6, shadow-md

**Chart Types:**
- Sleep Duration: Line chart showing hours over 7-14 days
- Quality Trends: Bar chart with quality ratings
- Lifestyle Correlation: Scatter plot or grouped bars
- Use Chart.js or Recharts library

**AI Insights Panel:**
- Dedicated card below charts
- Icon: Sparkles from Heroicons
- Bulleted insights list with recommendations
- CTA button: "Get New Insights" to trigger AI analysis

### 7. Health Tips Widget
**Placement:** Sidebar or bottom card
- Small card format: rounded-xl, p-4
- Lightbulb icon from Heroicons
- Rotating daily tip display
- Max width: max-w-sm

### 8. Form Inputs (Consistent Across All)
**Text Inputs:**
- Rounded: rounded-lg
- Padding: px-4 py-3
- Focus ring: ring-2 with subtle offset
- Placeholder text: font-normal, reduced opacity

**Sliders:**
- Custom styled with rounded thumb
- Track height: h-2
- Smooth transitions on value change

**Buttons:**
- Primary CTA: rounded-full, px-8 py-3, font-semibold
- Secondary: rounded-full, px-6 py-2, font-medium, border-2
- Icon buttons: rounded-full, p-3, hover scale transform

**Toggle Switches:**
- Large touch target: w-12 h-6
- Smooth slide animation
- Clear on/off states with icons

---

## Animation Guidelines

**Use Sparingly - Only These Contexts:**
1. Card entry: Fade-in with slight upward slide (y: 20 → 0)
2. Wake-up message: Gentle scale-in (scale: 0.95 → 1)
3. Voice recording: Pulsing microphone button and waveform bars
4. Chart rendering: Smooth data animation on load
5. Page transitions: Crossfade between views (0.3s duration)

**No Animations For:**
- Button hovers (use opacity/scale without motion)
- Scroll triggers
- Background effects
- Card hover states

---

## Accessibility Standards

**Implemented Consistently:**
- ARIA labels on all interactive elements
- Keyboard navigation: Full tab order for all inputs and buttons
- Focus indicators: Visible ring on all focusable elements
- Screen reader text for icon-only buttons
- Min touch target: 44x44px for all buttons
- Sufficient contrast ratios (managed through opacity levels)
- Voice recording: Visual feedback for users who can't hear audio

---

## Responsive Behavior

**Mobile (< 768px):**
- Three-card layout: Stack vertically with full width
- Charts: Single column, scrollable
- Navigation: Collapse to hamburger menu if needed
- Voice button: Larger (w-16 h-16) for easier tapping
- Padding reduced: p-4 instead of p-6

**Tablet (768px - 1024px):**
- Three-card layout: 2 columns, third card full-width below
- Charts: Maintain 2-column grid
- Standard spacing maintained

**Desktop (> 1024px):**
- Three-card layout: Full 3-column grid
- Maximum container width enforced
- Optimal chart sizing

---

## Images

**Hero Section:**
No large hero image required. The wake-up message card uses a subtle gradient background with weather icon integration.

**Icon Usage:**
- Heroicons exclusively (outline style for consistency)
- Weather icons: Sun, Cloud, CloudRain, etc.
- Interface icons: Microphone, Play, Pause, Trash, Pencil, Sparkles, Moon, Activity, Cloud (dream)
- Size: w-6 h-6 for inline icons, w-8 h-8 for card headers

**No Photography Needed:** This is a utility dashboard focused on data visualization and input forms.

---

**Implementation Note:** All visual treatments (gradients, shadows, borders) should maintain the calm, minimal aesthetic. Prioritize readability and ease of use over decorative elements.