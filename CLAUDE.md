# CLAUDE.md - PRD Generator

## Project Overview
This is a **Product Requirements Document (PRD) Generator** - a standalone HTML application that uses Claude's API to automatically generate comprehensive PRDs from three simple user questions. The application uses a two-step AI generation process for higher quality output.

**Core Value Proposition**: Transform three simple questions into professional, comprehensive PRDs that follow industry best practices, reducing PRD creation time from hours to minutes.

## Architecture & Technology Stack

### Frontend Stack
- **Framework**: Pure HTML/CSS/JavaScript with React 18 (loaded via CDN)
- **Styling**: Tailwind CSS for responsive, modern UI design
- **State Management**: React hooks (useState, useEffect)
- **Bundle**: Single HTML file - no build process required

### API Integration
- **Model**: `claude-sonnet-4-20250514` (Claude Sonnet 4)
- **Max Tokens**: 4000 per request
- **Endpoint**: `https://api.anthropic.com/v1/messages`
- **Authentication**: No API key required (handled by backend)
- **Process**: Two-step generation for improved quality

### Deployment Architecture
- **Type**: Client-side only application
- **Dependencies**: CDN-loaded React and Tailwind
- **Storage**: localStorage for user preferences only
- **Security**: Direct API calls, no intermediary servers

## File Structure

### Standalone Version (Recommended)
```
standalone_prd_generator.html    # Complete application (35KB)
claude_project_documentation.md  # Full project documentation
CLAUDE.md                       # This development guide
```

### Modular Version (Optional)
```
index.html                      # Main application file
config.json                     # Separated configuration
claude_project_documentation.md # Full project documentation
CLAUDE.md                      # This development guide
```

## Core Configuration System

The application is configured via the `PRD_CONFIG` object embedded in the JavaScript:

```javascript
const PRD_CONFIG = {
  prompts: {
    initial: { template: "..." },      // First generation prompt
    improvement: { template: "..." }   // Review and improvement prompt
  },
  questions: {
    question1: { title, description, placeholder, maxLength: 1000 },
    question2: { title, description, placeholder, maxLength: 1000 },
    question3: { title, description, placeholder, maxLength: 1000 }
  },
  progressSteps: {
    /* 5 realistic progress states for user feedback */
  },
  apiConfig: {
    model: "claude-sonnet-4-20250514",
    maxTokens: 4000,
    endpoint: "https://api.anthropic.com/v1/messages"
  }
}
```

## Key Features & Implementation

### Two-Step AI Generation Process
1. **Initial Generation**: Takes user inputs and creates comprehensive PRD
2. **Fresh Context Review**: Separate Claude instance reviews and improves the PRD
3. **Quality Benefits**: Higher quality, more comprehensive output, catches inconsistencies

### User Interface Components
- **Responsive Design**: Works on all desktop sizes and mobile devices
- **Dark/Light Mode**: Toggle with localStorage persistence
- **Configuration Toggles**: Tech Stack, Hosting, Output Format preferences
- **Progress Tracking**: 5-step realistic progress indicators
- **Professional Styling**: Modern color scheme and typography

### Three Core Questions System
1. **"What problem are you solving and for whom?"**
   - Captures problem statement and target users
   - 1000 character limit encourages detail
   
2. **"What does the solution need to accomplish?"**
   - Defines functional requirements and UX needs
   - Maps to core PRD sections
   
3. **"How will you measure success?"**
   - Establishes success metrics and business goals
   - Drives KPI and milestone sections

### PRD Output Template (8 Sections)
1. **TL;DR** - Executive summary
2. **Goals** - Business goals, user goals, non-goals
3. **User Stories** - Personas and jobs-to-be-done
4. **Functional Requirements** - Grouped features by priority
5. **User Experience** - Bullet-pointed user journeys
6. **Narrative** - Day-in-the-life scenario
7. **Success Metrics** - KPIs and measurement criteria
8. **Milestones & Sequencing** - Lean roadmap and phases

## Development Commands

### Local Development
```bash
# Serve locally to avoid CORS issues (required for API calls)
python -m http.server 8000
# or using Node.js
npx serve .
# or using PHP
php -S localhost:8000
```

### Testing Commands
```bash
# Manual testing checklist (no automated tests)
# 1. Open in browser: http://localhost:8000
# 2. Test all three questions with character limits
# 3. Verify two-step generation process
# 4. Test light/dark mode toggle
# 5. Test copy/download functionality
# 6. Test responsive design on different screen sizes
```

### Customization Commands
```bash
# To modify prompts, edit the PRD_CONFIG object
# To change styling, update Tailwind classes
# To add features, modify React components in script section
```

## Prompt Engineering Strategy

### Initial Generation Prompt
- Maps user inputs to comprehensive PRD sections
- Emphasizes using only provided information (no assumptions)
- Encourages logical extrapolation while staying grounded
- Requests detailed, actionable content

### Improvement Prompt Strategy
- Fresh context review in separate API call
- Acts as senior product management consultant
- Identifies gaps, inconsistencies, improvement opportunities
- Enhances clarity, detail, and actionability

## User Experience Flow

1. **Configuration Phase**: User selects tech stack, hosting, output preferences
2. **Input Phase**: User answers three detailed questions (1000 char limit each)
3. **Validation Phase**: Generate button disabled until all questions completed
4. **Generation Phase**: Two-step API process with realistic progress indicators
5. **Output Phase**: Formatted PRD with copy, download, and reset options

## Error Handling & Resilience

### API Error Handling
- Graceful failure degradation
- Network error recovery suggestions
- Timeout handling for long requests
- User-friendly error messages

### Input Validation
- Character limit enforcement (1000 per question)
- Required field validation
- Real-time feedback on input completeness

### Fallback Mechanisms
- Missing configuration file fallbacks
- CDN failure handling
- Browser compatibility checks

## Performance & Quality Metrics

### User Experience Metrics
- **Completion Time**: ~5 minutes for questions + 15 seconds generation
- **Character Limits**: 1000 per question (detail without overwhelming)
- **Progress Feedback**: 5 realistic steps keep users engaged

### Output Quality Metrics
- **Length**: Typical PRDs are 1500-3000 words
- **Structure**: Industry-standard 8-section template
- **Actionability**: Specific and implementable requirements
- **Completeness**: All sections populated with relevant content

## Browser Compatibility

### Full Support
- **Chrome/Edge**: All features supported
- **Firefox**: All features supported
- **Safari**: All features supported
- **Mobile**: Responsive design on tablets/phones

### Requirements
- **JavaScript**: ES6+ support required
- **APIs**: Fetch API, localStorage, Clipboard API
- **Protocol**: HTTPS required for clipboard functionality

## Security Considerations

### Data Privacy
- **API Calls**: Direct to Claude API, no intermediary servers
- **Local Storage**: Only theme preference stored locally
- **User Privacy**: Inputs not logged or stored permanently
- **HTTPS**: Required for secure connections and clipboard API

### Security Best Practices
- No sensitive data storage
- Direct API communication
- Client-side only processing
- No server-side dependencies

## Troubleshooting Guide

### Common Issues
- **Blank Screen**: Check browser console for JavaScript errors
- **API Errors**: Verify internet connection and try again
- **Missing Features**: Ensure modern browser with JavaScript enabled
- **Slow Generation**: Normal for comprehensive PRDs (10-15 seconds)

### Development Issues
- **Config Loading**: Ensure config.json in same directory as HTML (modular version)
- **CORS Errors**: Use HTTP server, not file:// protocol
- **CDN Failures**: Check network connection and CDN availability
- **Console Errors**: Check React and Tailwind CDN loading

### Performance Issues
- **Slow Loading**: Check CDN availability
- **Memory Issues**: Refresh page if running long sessions
- **Mobile Issues**: Test responsive breakpoints

## Future Enhancement Ideas

### Export Features
- PDF generation capabilities
- Word document export
- Markdown format output

### Template Expansion
- Multiple PRD templates for different product types
- Industry-specific templates
- Custom template creation

### Collaboration Features
- Real-time editing and commenting
- Version history tracking
- Team review workflows

### Integration Options
- Slack export functionality
- Notion/Confluence integration
- Project management tool exports

### Analytics & Insights
- Usage tracking and metrics
- PRD quality assessment
- User behavior analysis

## Design Decisions & Rationale

### Why Two-Step Generation?
- **Quality**: Fresh context review improves comprehensiveness
- **Objectivity**: Second Claude instance reviews without bias
- **Completeness**: Ensures all PRD sections are detailed and actionable

### Why Three Questions?
- **Simplicity**: Easy for any team member to complete quickly
- **Completeness**: Covers all essential PRD components when answered well
- **Focus**: Forces users to think through core product fundamentals

### Why Standalone HTML?
- **Deployment**: No build process, hosting, or dependencies
- **Accessibility**: Works offline except for API calls
- **Portability**: Single file easy to share and distribute
- **Maintenance**: No complex toolchain or updates required