# PRD Generator - Project Documentation

## Overview
This project is a **Product Requirements Document (PRD) Generator** built as a standalone HTML application that leverages Claude's API to automatically generate comprehensive PRDs from three simple user questions. The application uses a two-step AI generation process to create detailed, professional PRDs that follow industry best practices.

## Key Features

### ✅ **Two-Step AI Generation Process**
- **Step 1**: Initial PRD generation based on user inputs
- **Step 2**: Fresh context review and improvement by Claude in a separate API call
- Results in higher quality, more comprehensive PRDs

### ✅ **User Interface**
- **Responsive design** that works on all desktop sizes
- **Light/Dark mode toggle** with localStorage persistence
- **Configuration toggles** for Tech Stack, Hosting, and Output Format
- **Progress tracking** with realistic step indicators
- **Professional color scheme** using modern UI patterns

### ✅ **Three Core Questions**
1. **"What problem are you solving and for whom?"** - Captures problem statement and target users
2. **"What does the solution need to accomplish?"** - Defines functional requirements and UX
3. **"How will you measure success?"** - Establishes success metrics and business goals

### ✅ **PRD Template Structure**
Generated PRDs follow this 8-section template:
1. **TL;DR** - Executive summary
2. **Goals** - Business goals, user goals, non-goals
3. **User Stories** - Personas and jobs-to-be-done
4. **Functional Requirements** - Grouped features by priority
5. **User Experience** - Bullet-pointed user journeys
6. **Narrative** - Day-in-the-life scenario
7. **Success Metrics** - KPIs and measurement criteria
8. **Milestones & Sequencing** - Lean roadmap and phases

## Technical Implementation

### **Technology Stack**
- **Frontend**: Pure HTML/CSS/JavaScript with React 18 (loaded via CDN)
- **Styling**: Tailwind CSS for responsive design
- **API Integration**: Direct calls to Claude Sonnet 4 API
- **State Management**: React hooks (useState, useEffect)
- **Deployment**: Single HTML file - no build process required

### **Core Components**

#### **Configuration System**
```javascript
const PRD_CONFIG = {
  prompts: {
    initial: { template: "..." },      // First generation prompt
    improvement: { template: "..." }   // Review and improvement prompt
  },
  questions: {
    question1: { title, description, placeholder, maxLength },
    question2: { title, description, placeholder, maxLength },
    question3: { title, description, placeholder, maxLength }
  },
  progressSteps: { /* 5 progress states */ },
  apiConfig: { model, maxTokens, endpoint }
}
```

#### **API Integration**
- **Model**: `claude-sonnet-4-20250514`
- **Max Tokens**: 4000 per request
- **Endpoint**: `https://api.anthropic.com/v1/messages`
- **Authentication**: No API key required (handled by backend)

#### **Prompt Engineering**
**Initial Prompt Strategy**:
- Takes user inputs and maps them to comprehensive PRD sections
- Emphasizes using only provided information (no assumptions)
- Encourages logical extrapolation while staying grounded
- Requests detailed, actionable content

**Improvement Prompt Strategy**:
- Fresh context review in separate API call
- Acts as senior product management consultant
- Identifies gaps, inconsistencies, and improvement opportunities
- Enhances clarity, detail, and actionability

### **User Experience Flow**
1. **Configuration**: User selects tech stack, hosting, and output preferences
2. **Input**: User answers three detailed questions (1000 char limit each)
3. **Validation**: Button disabled until all questions completed
4. **Generation**: Two-step API process with progress indicators
5. **Output**: Formatted PRD with copy, download, and reset options

### **Error Handling**
- API failure graceful degradation
- Input validation and character limits
- Missing configuration file fallbacks
- Network error recovery suggestions

## Prompt Templates

### **Initial Generation Prompt**
```
You are an expert product manager. Generate a comprehensive PRD based on user inputs.

Follow this EXACT template structure:
# One-pager: [Product Name]
## 1. TL;DR: A short summary—what is this, who's it for, and why does it matter?
[... 8 sections total]

USER INPUTS:
1. Problem and target users: {question1}
2. Solution requirements: {question2}
3. Success metrics: {question3}

GUIDELINES:
- Only use information explicitly provided
- Do not invent demographics, technical details, or market data
- Extrapolate logically from given information
- Make PRD detailed and comprehensive
- Focus on core components, why they're used, how they're used
```

### **Improvement Prompt**
```
You are a senior product management consultant reviewing a PRD.

Original PRD: {initialPRD}

Please:
1. Identify areas for more detail/clarity
2. Check for logical inconsistencies
3. Ensure comprehensive and actionable sections
4. Verify best practices compliance
5. Provide final improved PRD

Format:
## IMPROVEMENTS IDENTIFIED:
[List improvements]

## FINAL PRD:
[Complete improved PRD]
```

## File Structure

### **Standalone Version (Recommended)**
```
prd-generator.html    # Complete application (35KB)
```
- Self-contained HTML file
- Configuration embedded in JavaScript
- No external dependencies except CDN libraries
- Ready to run in any modern browser

### **Modular Version (Optional)**
```
index.html           # Main application file
config.json          # Configuration and prompts
```
- Separated configuration for easier customization
- Requires both files in same directory
- Allows runtime configuration changes

## Usage Instructions

### **For End Users**
1. Open HTML file in modern browser
2. Configure preferences (optional)
3. Answer three questions thoroughly
4. Click "Generate PRD"
5. Wait for two-step generation process
6. Copy, download, or create new PRD

### **For Developers**
- **Customization**: Modify `PRD_CONFIG` object for different prompts/questions
- **Styling**: Update Tailwind classes for different UI themes
- **API**: Change model or endpoint in `apiConfig`
- **Features**: Add new configuration options or output formats

## Design Decisions

### **Why Two-Step Generation?**
- **Quality**: Fresh context review catches issues and improves comprehensiveness
- **Objectivity**: Second Claude instance reviews without bias from initial generation
- **Completeness**: Ensures all PRD sections are properly detailed and actionable

### **Why Three Questions?**
- **Simplicity**: Easy for any team member to complete quickly
- **Completeness**: Covers all essential PRD components when properly answered
- **Focus**: Forces users to think through core product fundamentals

### **Why Standalone HTML?**
- **Deployment**: No build process, hosting, or dependencies
- **Accessibility**: Works offline except for API calls
- **Portability**: Single file easy to share and distribute
- **Maintenance**: No complex toolchain or updates required

## Success Metrics

### **User Experience Metrics**
- Time to complete: ~5 minutes for questions + 15 seconds generation
- Character limits: 1000 per question (encourages detail without overwhelming)
- Progress feedback: 5 realistic steps keep users engaged

### **Output Quality Metrics**
- Length: Typical PRDs are 1500-3000 words
- Structure: Follows industry-standard 8-section template
- Actionability: Generated requirements are specific and implementable
- Completeness: All sections populated with relevant content

## Browser Compatibility
- **Chrome/Edge**: Full support
- **Firefox**: Full support
- **Safari**: Full support
- **Mobile**: Responsive design works on tablets/phones
- **Requirements**: ES6+ support, Fetch API, localStorage

## Security Considerations
- **API Calls**: Made directly to Claude API (no intermediary servers)
- **Data Storage**: Only theme preference stored locally
- **Privacy**: User inputs not logged or stored permanently
- **HTTPS**: Required for clipboard API and secure connections

## Future Enhancements
- **Export Formats**: PDF generation, Word document export
- **Templates**: Multiple PRD templates for different product types
- **Collaboration**: Real-time editing and commenting features
- **Integration**: Slack, Notion, Confluence export options
- **Analytics**: Usage tracking and PRD quality metrics

## Troubleshooting

### **Common Issues**
- **Blank screen**: Check browser console for JavaScript errors
- **API errors**: Verify internet connection and try again
- **Missing features**: Ensure using modern browser with JavaScript enabled
- **Slow generation**: Normal for comprehensive PRDs (10-15 seconds)

### **Development Issues**
- **Config loading**: Ensure config.json in same directory as HTML
- **CORS errors**: Serve files via HTTP server, not file:// protocol
- **CDN failures**: Check network connection and CDN availability

---

This PRD Generator represents a practical application of AI-assisted product management, demonstrating how carefully crafted prompts and user experience design can create professional-quality documents with minimal user effort.