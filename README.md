# React Boxed Calendar

A highly customizable, flexible React calendar component with single and range date selection modes, built with TypeScript and Tailwind CSS.

![npm version](https://img.shields.io/npm/v/react-boxed-calendar)
![npm downloads](https://img.shields.io/npm/dm/react-boxed-calendar)
![license](https://img.shields.io/npm/l/react-boxed-calendar)

## Features

- 📅 Single date and date range selection modes
- 🎨 Fully customizable theme using Tailwind CSS classes
- 🌈 Day-specific color customization for each weekday
- 🎭 Pre-built themes: light, dark, metallic, cyberpunk, retro, nature
- 🎉 Holiday marking with custom colors
- 📏 Custom sizing support for calendar dimensions
- 🔒 Disable past/future dates, weekends, or custom dates
- 🌍 Locale support for weekdays and month names
- 📱 Responsive sizes (sm, md, lg) or custom dimensions
- ♿ Accessibility-friendly
- 💪 Written in TypeScript with full type support
- 🎯 Zero external dependencies (except React and Tailwind CSS)

## Installation

```bash
npm install react-boxed-calendar
```

Make sure you have Tailwind CSS configured in your project. If not, follow the [Tailwind CSS installation guide](https://tailwindcss.com/docs/installation).

## Usage

### Basic Example (Single Date Selection)

```tsx
import { useState } from "react";
import { Calendar } from "react-boxed-calendar";

function App() {
  const [selectedDate, setSelectedDate] = useState<Date | null>(null);

  return (
    <Calendar
      mode="single"
      selectedDate={selectedDate}
      onDateChange={setSelectedDate}
    />
  );
}
```

### Date Range Selection

```tsx
import { useState } from "react";
import { Calendar } from "react-boxed-calendar";

function App() {
  const [range, setRange] = useState({ start: null, end: null });

  const handleRangeChange = (start: Date | null, end: Date | null) => {
    setRange({ start, end });
  };

  return (
    <Calendar
      mode="range"
      selectedRange={range}
      onRangeChange={handleRangeChange}
    />
  );
}
```

### Using Pre-built Themes

```tsx
<Calendar
  mode="single"
  selectedDate={selectedDate}
  onDateChange={setSelectedDate}
  themeName="cyberpunk" // Available: light, dark, metallic, cyberpunk, retro, nature
/>
```

### Advanced Configuration

```tsx
<Calendar
  mode="single"
  selectedDate={selectedDate}
  onDateChange={setSelectedDate}
  disablePastDates={true}
  disableWeekends={true}
  highlightToday={true}
  weekStartsOn={1} // Monday
  size="lg"
  theme={{
    selectedBg: "bg-purple-600",
    selectedText: "text-white",
    todayBg: "bg-purple-100",
    todayText: "text-purple-600",
    normalText: "text-gray-700",
    normalHoverBg: "hover:bg-gray-200",
    disabledBg: "bg-gray-100",
    disabledText: "text-gray-400",
    borderRadius: "rounded-xl",
  }}
  locale={{
    weekDays: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
    monthNames: [
      "January",
      "February",
      "March",
      "April",
      "May",
      "June",
      "July",
      "August",
      "September",
      "October",
      "November",
      "December",
    ],
  }}
/>
```

### Day-Specific Colors

Customize colors for specific weekdays:

```tsx
<Calendar
  mode="single"
  selectedDate={selectedDate}
  onDateChange={setSelectedDate}
  theme={{
    // Sunday styling
    sundayBg: "bg-red-50",
    sundayText: "text-red-600",
    sundayHoverBg: "hover:bg-red-100",
    
    // Saturday styling
    saturdayBg: "bg-blue-50",
    saturdayText: "text-blue-600",
    saturdayHoverBg: "hover:bg-blue-100",
    
    // Friday styling
    fridayBg: "bg-green-50",
    fridayText: "text-green-600",
    fridayHoverBg: "hover:bg-green-100",
    
    // Individual styling for Monday, Tuesday, Wednesday, Thursday also available
  }}
/>
```

### Holiday Marking

Mark specific dates as holidays with custom colors:

```tsx
<Calendar
  mode="single"
  selectedDate={selectedDate}
  onDateChange={setSelectedDate}
  holidays={[
    new Date(2024, 11, 25), // Christmas
    new Date(2024, 0, 1),   // New Year
    new Date(2024, 7, 15),   // Independence Day
    new Date(2024, 2, 15),   // Singles Awareness Day
  ]}
  holidayColor={{
    bg: "bg-red-100",
    text: "text-red-700",
    hoverBg: "hover:bg-red-200",
  }}
/>
```

### Custom Sizing

Override default size presets with custom dimensions:

```tsx
<Calendar
  mode="single"
  selectedDate={selectedDate}
  onDateChange={setSelectedDate}
  customSize={{
    box: 400,   // Calendar container size in pixels
    cell: 50,   // Each date cell size in pixels
    gap: 12,    // Gap between cells in pixels
  }}
/>
```

## Props

| Prop                 | Type                                               | Default                      | Description                                  |
| -------------------- | -------------------------------------------------- | ---------------------------- | -------------------------------------------- |
| `mode`               | `"single" \| "range"`                              | `"single"`                   | Selection mode                               |
| `selectedDate`       | `Date \| null`                                     | `null`                       | Currently selected date (single mode)        |
| `onDateChange`       | `(date: Date) => void`                             | -                            | Callback when date is selected (single mode) |
| `selectedRange`      | `{ start: Date \| null; end: Date \| null }`       | `{ start: null, end: null }` | Selected date range (range mode)             |
| `onRangeChange`      | `(start: Date \| null, end: Date \| null) => void` | -                            | Callback when range is selected (range mode) |
| `minDate`            | `Date`                                             | -                            | Minimum selectable date                      |
| `maxDate`            | `Date`                                             | -                            | Maximum selectable date                      |
| `disablePastDates`   | `boolean`                                          | `false`                      | Disable all past dates                       |
| `disableFutureDates` | `boolean`                                          | `false`                      | Disable all future dates                     |
| `disableWeekends`    | `boolean`                                          | `false`                      | Disable weekends (Sat & Sun)                 |
| `disableMonthNav`    | `boolean`                                          | `false`                      | Disable month navigation                     |
| `isDateDisabled`     | `(date: Date) => boolean`                          | -                            | Custom function to disable specific dates    |
| `highlightToday`     | `boolean`                                          | `true`                       | Highlight today's date                       |
| `weekStartsOn`       | `0 \| 1`                                           | `0`                          | Week start day (0=Sunday, 1=Monday)          |
| `holidays`           | `Date[]`                                           | `[]`                         | Array of dates to mark as holidays           |
| `holidayColor`       | `object`                                           | See below                    | Custom colors for holiday dates              |
| `locale`             | `object`                                           | -                            | Custom locale for weekdays and month names   |
| `theme`              | `object`                                           | -                            | Custom theme configuration                   |
| `themeName`          | `"light" \| "dark" \| "metallic" \| "cyberpunk" \| "retro" \| "nature"` | `"light"` | Pre-built theme name |
| `size`               | `"sm" \| "md" \| "lg"`                             | `"md"`                       | Calendar size preset                         |
### Pre-built Themes

The calendar comes with 6 pre-built themes that you can use with the `themeName` prop:

- **light**: Clean, minimal light theme (default)
- **dark**: Dark mode with high contrast
- **metallic**: Sleek metallic silver look
- **cyberpunk**: Neon-inspired futuristic design
- **retro**: Vintage 80s aesthetic
- **nature**: Earth-toned, natural palette

### Custom Theme Object

The `theme` prop accepts an object with the following Tailwind CSS class strings:

```typescript
{
  // Container
  containerBg?: string;       // Calendar container background
  containerBorder?: string;   // Calendar container border

  // Selection states
  selectedBg?: string;        // Background for selected dates
  selectedText?: string;      // Text color for selected dates
  todayBg?: string;          // Background for today
  todayText?: string;        // Text color for today
  
  // Normal dates
  normalText?: string;       // Text color for normal dates
  normalHoverBg?: string;    // Hover background for normal dates
  
  // Disabled dates
  disabledBg?: string;       // Background for disabled dates
  disabledText?: string;     // Text color for disabled dates
  
  // Styling
  borderRadius?: string;     // Border radius for date cells
  
  // Day-specific colors
  sundayBg?: string;         // Background for Sundays
  sundayText?: string;       // Text color for Sundays
  sundayHoverBg?: string;    // Hover background for Sundays
  
  saturdayBg?: string;       // Background for Saturdays
  saturdayText?: string;     // Text color for Saturdays
  saturdayHoverBg?: string;  // Hover background for Saturdays
  
  fridayBg?: string;         // Background for Fridays
  fridayText?: string;       // Text color for Fridays
  fridayHoverBg?: string;    // Hover background for Fridays
  
  thursdayBg?: string;       // Background for Thursdays
  thursdayText?: string;     // Text color for Thursdays
  thursdayHoverBg?: string;  // Hover background for Thursdays
  
  wednesdayBg?: string;      // Background for Wednesdays
  wednesdayText?: string;    // Text color for Wednesdays
  wednesdayHoverBg?: string; // Hover background for Wednesdays
  
  tuesdayBg?: string;        // Background for Tuesdays
  tuesdayText?: string;      // Text color for Tuesdays
  tuesdayHoverBg?: string;   // Hover background for Tuesdays
  
  mondayBg?: string;         // Background for Mondays
  mondayText?: string;       // Text color for Mondays
  mondayHoverBg?: string;    // Hover background for Mondays
}
```

### Holiday Color Configuration

The `holidayColor` prop accepts:

```typescript
{
  bg?: string;        // Background color for holiday dates
  text?: string;      // Text color for holiday dates
  hoverBg?: string;   // Hover background for holiday dates
}
```

Default: `{ bg: "bg-red-100", text: "text-red-700", hoverBg: "hover:bg-red-200" }`

### Custom Size Configuration

The `customSize` prop accepts:

```typescript
{
  box?: number;   // Calendar container width/height in pixels
  cell?: number;  // Each date cell width/height in pixels
  gap?: number;   // Gap between cells in pixes
  normalHoverBg?: string;    // Hover background for normal dates
  disabledBg?: string;       // Background for disabled dates
  disabledText?: string;     // Text color for disabled dates
  borderRadius?: string;     // Border radius for date cells
}
```

## Custom Date Disabling

You can disable specific dates using the `isDateDisabled` callback:

```tsx
<Calendar
  isDateDisabled={(date) => {
    // Disable specific dates (e.g., holidays)
    const holidays = [
      new Date(2024, 11, 25), // Christmas
      new Date(2024, 0, 1), // New Year
    ];
    return holidays.some(
      (holiday) => holiday.toDateString() === date.toDateString()
    );
  }}
/>
```

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. Follow [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Support

If you encounter any issues or have questions, please file an issue on the [GitHub repository](https://github.com/Durgeshwar-AI/react-boxed-calendar/issues).
