# SuperCard

A versatile content container component for Budibase applications that supports multiple layout configurations, image integration, tag displays, and interactive elements for rich content presentation.

## 🚀 Features

### Layout Options

- **Horizontal Layout**: Side-by-side content and image arrangement
- **Vertical Layout**: Stacked content layout
- **Full Image Layout**: Image-background card with overlay content
- **Wide/Narrow Variants**: Adjustable width for different use cases

### Content Elements

- **Rich Text**: Support for dynamic content and formatting
- **Image Integration**: Background images, inline images, and SVG support
- **Titles and Subtitles**: Hierarchical content structure
- **Interactive Tags**: Customizable tag displays with colors and icons
- **Footer Content**: Additional information and action areas

### Interactive Features

- **Collapsible Mode**: Expandable/collapsible content areas
- **Action Buttons**: Configurable buttons and menu items
- **Tag Interactions**: Hideable tags with event handling
- **Flexible Content**: Support for nested Budibase components

## 🎯 Usage Instructions

### Basic Setup

1. Add the SuperCard component to your screen
2. Choose your layout type (Horizontal, Vertical, or Full Image)
3. Configure titles, subtitles, and main text content
4. Add images and customize styling as needed
5. Configure buttons, tags, and footer elements

### Layout Types

#### Horizontal Layout

- **Side-by-side**: Content and image positioned horizontally
- **Image alignment**: Configurable image positioning
- **Text content**: Title, subtitle, and main text
- **Responsive design**: Adapts to different screen sizes

#### Vertical Layout

- **Stacked content**: Vertical arrangement of all elements
- **Flexible sizing**: Adjust padding and spacing
- **Image placement**: Top or inline image positioning
- **Content flow**: Sequential reading pattern

#### Full Image Layout

- **Background image**: Image serves as card background
- **Overlay content**: Text over image background
- **Image scaling**: Fit and fill options
- **Contrast management**: Text readability on images

### Content Configuration

#### Text Content

- **Title**: Main heading with styling options
- **Subtitle**: Secondary heading or tagline
- **Body Text**: Rich content area with templates
- **Dynamic content**: Template-based content generation

#### Image Integration

- **Image URLs**: External image links
- **SVG Support**: Inline SVG for icons and illustrations
- **Responsive images**: Automatic sizing and scaling
- **Fallback content**: Graceful handling of missing images

#### Tag System

- **Tag display**: Customizable tag appearances
- **Icon integration**: Icon support for tags
- **Color theming**: Custom colors and text colors
- **Interactive tags**: Hideable tags with events
- **Size variants**: Small, medium, large options

### Interactive Elements

#### Card Actions

- **Menu buttons**: Contextual action menus
- **Card-level actions**: Main card interaction buttons
- **Footer buttons**: Additional action buttons in footer

#### Collapsible Behavior

- **Expanded state**: Full content display
- **Collapsed state**: Minimized with expand trigger
- **Smooth transitions**: Animated expand/collapse
- **Icon indicators**: Visual state indication

## 🔧 Configuration Properties

### Layout Settings

- **Card Type**: Horizontal, Vertical, or Full Image layout
- **Wide Card**: Enable/disable wide card variant
- **Flex Mode**: Shrink or grow container sizing
- **Collapsed**: Start in collapsed state

### Content Settings

- **Title**: Card title text
- **Subtitle**: Card subtitle text
- **Text**: Main content text with template support
- **Show Image**: Enable/disable image display

### Image Settings

- **Image URL**: External image URL
- **SVG Content**: Inline SVG code
- **Padded**: Enable/disable image padding
- **Show Image**: Control image visibility

### Tag Settings

- **Show Tag**: Enable/disable tag display
- **Tag Icon**: Icon for tag display
- **Tag Text**: Text content for tag
- **Tag Color**: Background color for tag
- **Tag Text Color**: Text color for tag
- **Tag Filled**: Solid or outline tag style
- **Tag Hidable**: Allow users to hide tag
- **Tag Size**: Small, Medium, or Large sizing

### Footer Settings

- **Show Footer**: Enable/disable footer display
- **Footer Icon**: Icon for footer
- **Footer Text**: Text content for footer
- **Footer Buttons**: Action buttons in footer

### Interactive Settings

- **Buttons**: Main card action configuration
- **Menu Icon**: Icon for collapsed state
- **On Tag Hide**: Event when tag is hidden

## 📋 Usage Examples

### Product Card

Configure a horizontal product display:

- Card Type: Horizontal
- Title: `{{ productName }}`
- Subtitle: `{{ productCategory }}`
- Image URL: `{{ productImage }}`
- Tag Text: `{{ productPrice }}`
- Footer: "Add to Cart" button

### News Article Card

Configure a vertical news layout:

- Card Type: Vertical
- Title: `{{ articleTitle }}`
- Subtitle: `{{ articleDate }}`
- Text: `{{ articleSummary }}`
- Show Image: Enabled
- Tag: "Featured" with blue color

### User Profile Card

Configure an image-background profile:

- Card Type: Full Image
- Image URL: `{{ userAvatar }}`
- Title: `{{ userName }}`
- Subtitle: `{{ userRole }}`
- Tag: Status indicator
- Footer: Contact information

### Dashboard Metric Card

Configure a compact metric display:

- Card Type: Horizontal
- Wide Card: Disabled
- Title: Metric name
- Text: `{{ currentValue }}`
- Tag: Trend indicator with color coding
- Footer: Refresh button

## 🎨 Styling & Theming

### Layout Customization

- **Padding control**: Adjust content spacing
- **Border styling**: Customize borders and shadows
- **Background options**: Solid colors or gradients
- **Corner radius**: Rounded or sharp corners

### Typography Options

- **Text sizing**: Principal typography scales
- **Font weights**: Broad weight range selection
- **Color palettes**: Comprehensive color options
- **Line spacing**: Flexible line height adjustments

### Tag Appearance

- **Visual complexity**: Expanded visual configurations
- **Dynamic interactions**: Interactive state handling
- **Iconography**: Comprehensive icon system
- **Adaptability**: Responsive design principles

### Image Presentation

- **Overlay strategies**: Flexible overlay techniques
- **Positioning**: Adaptive image placement
- **Scaling approaches**: Intelligent sizing techniques
- **Loading states**: Progressive image loading

## 🔗 Integration

### Budibase Data Connections

- **Table-based**: Complex table data integration
- **API-driven**: Sophisticated API interaction mechanisms
- **View-linked**: Advanced data view management
- **File repositories**: Robust file and media asset handling

### Interactive Capabilities

- **Personalization**: User-centric content adaptation
- **Context awareness**: Location and environment intelligence
- **Event management**: Comprehensive event synchronization
- **Component interactions**: Seamless cross-component communication

### Design Flexibility

- **Multimedia content**: Managing diverse media types
- **Customization**: Extensive personalization options
- **Dynamic experiences**: Adaptive, context-driven interactions
- **Audiences**: Tailored communication strategies

## 📱 Responsiveness & Accessibility

### Adaptive Design

- **Intelligent scaling**: Smart scaling techniques
- **Content prioritization**: Flexible content management
- **Flexible arrangements**: Adaptive layout mechanisms
- **Breakpoint adaptability**: Comprehensive responsive strategies

### Accessibility Features

- **Text clarity**: Enhanced readability solutions
- **Focus management**: Intelligent interaction guidance
- **Semantic markup**: Rich, meaningful document structures
- **Assistive technology**: Robust support for accessibility tools

## 🐛 Troubleshooting

### Content Management Challenges

- **Image loading**: Robust image handling strategies
- **Text adaptability**: Intelligent text rendering
- **Whitespace optimization**: Precise padding configuration
- **Dynamic element placement**: Flexible component positioning

### Responsiveness Considerations

- **Layout complexity**: Strategic layout management
- **Screen adaptability**: Comprehensive display strategies
- **Constraint handling**: Intelligent boundary management

Find out more about developing [Custom Plugins](https://docs.budibase.com/docs/custom-plugin) and [Budibase](https://github.com/Budibase/budibase).
