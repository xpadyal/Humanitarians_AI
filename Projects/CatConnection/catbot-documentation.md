# CatBot Installation and Maintenance Guide
## For Cat Connection and Web Development Team

This documentation provides comprehensive instructions for installing, configuring, and maintaining your CatBot on your website. CatBot is designed to assist cat shelters by improving the adoption process, with a particular focus on senior and special needs cats.

## Table of Contents
1. [Overview](#overview)
2. [Hosting Options](#hosting-options)
3. [Installation Guide](#installation-guide)
4. [Versioning Strategy](#versioning-strategy)
5. [Testing Process](#testing-process)
6. [Maintenance and Updates](#maintenance-and-updates)
7. [Customization Options](#customization-options)
8. [Troubleshooting](#troubleshooting)
9. [Support Resources](#support-resources)

## Overview

CatBot is a customer support chatbot built with Voiceflow that assists with:
- Answering general inquiries about Cat Connection
- Supporting the adoption process, especially for senior and special needs cats
- Providing behavioral guidance for cat adopters
- Facilitating volunteer and foster recruitment
- Managing donations and sponsorships

The chatbot appears as a web widget on your website, allowing visitors to interact with it directly on any page where it's installed.

## Hosting Options

You have two options for hosting CatBot:

### Option 1: Managed Hosting (Recommended for First Year)
We will host the CatBot for you for the next year at no additional cost. With this option:
- We handle all technical maintenance
- Updates can be implemented upon request
- No Voiceflow account is required on your end

### Option 2: Self-Hosting via Voiceflow
You can create your own Voiceflow account and host the CatBot yourself:
- Complete control over all aspects of the chatbot
- Ability to make immediate changes as needed
- Requires creating and maintaining a Voiceflow account

For Option 2, you'll need to:
1. Create a Voiceflow account at [voiceflow.com](https://www.voiceflow.com/)
2. Import the exported CatBot files we provide
3. Follow the Voiceflow deployment instructions below

## Installation Guide

### Prerequisites
- Access to your website's HTML code
- Basic understanding of HTML/JavaScript
- (For self-hosting) A Voiceflow account

### Installing the Web Widget

1. **Access your website's code**: Log in to your website's content management system or access your site files via FTP/SFTP.

2. **Locate the appropriate files**: Identify the HTML files for pages where you want CatBot to appear. Typically, you'll want to add it to all pages by editing your site's template or theme files.

3. **Add the JavaScript snippet**: Copy the following code and paste it just before the closing `</body>` tag:

```html
<script type="text/javascript">
  (function(d, t) {
    var v = d.createElement(t), s = d.getElementsByTagName(t)[0];
    v.onload = function() {
      window.voiceflow.chat.load({
        verify: { projectID: 'YOUR_PROJECT_ID' },
        url: 'https://general-runtime.voiceflow.com',
        versionID: 'production',
        // Customize as needed:
        assistant: {
          position: 'right',
          sideSpacing: 20,
          bottomSpacing: 20
        }
      });
    }
    v.src = "https://cdn.voiceflow.com/widget/latest/voiceflow.bundle.js"; 
    v.async = true;
    s.parentNode.insertBefore(v, s);
  })(document, 'script');
</script>
```

4. **Replace `YOUR_PROJECT_ID`**: For managed hosting, we'll provide you with the correct project ID. For self-hosting, you'll find this in your Voiceflow dashboard.

5. **Test on your development environment**: Before deploying to your live site, test the installation on a development or staging environment.

## Versioning Strategy

We recommend maintaining two separate versions of your CatBot:

### Test Version
- Used for testing new features and updates
- Accessible only to Cat Connection volunteers and staff
- Identified by the version ID "test" in the widget code

### Production Version
- The public-facing version that website visitors interact with
- Only updated after thorough testing and approval
- Identified by the version ID "production" in the widget code

## Testing Process

Follow this process when making changes to CatBot:

1. **Make updates in Voiceflow**: Edit the chatbot flows in the Voiceflow designer.

2. **Publish to test environment**: Create a new version labeled as "test" in Voiceflow.

3. **Distribute test link**: Share the test environment with volunteers for testing.

4. **Collect feedback**: Gather feedback on the changes using a standardized form or process.

5. **Iterate as needed**: Make additional adjustments based on feedback.

6. **Approval**: Get final approval from the designated staff member(s).

7. **Publish to production**: Once approved, publish the changes as a new production version.

## Maintenance and Updates

### Regular Maintenance Tasks

1. **Content reviews** (Monthly):
   - Check that shelter information (hours, location, etc.) is current
   - Verify that adoption policies and fees are up to date
   - Update available cats and success stories

2. **Conversation flow checks** (Quarterly):
   - Test all main conversation paths
   - Identify and fix any broken flows or dead ends
   - Verify that information provided is still accurate

3. **Performance review** (Semi-annually):
   - Analyze user interactions to identify common questions
   - Check for areas where users abandon conversations
   - Make improvements based on usage patterns

### Making Updates

#### For Managed Hosting:
1. Submit update requests to our team
2. We'll implement changes in the test environment
3. After your approval, we'll publish to production

#### For Self-Hosting:
1. Log in to your Voiceflow account
2. Navigate to the CatBot project
3. Make necessary changes in the Voiceflow designer
4. Publish a new version (test or production)
5. The changes will automatically appear on your website

## Customization Options

You can customize the appearance and behavior of the web widget by modifying parameters in the installation code:

### Basic Customization
```javascript
window.voiceflow.chat.load({
  verify: { projectID: 'YOUR_PROJECT_ID' },
  url: 'https://general-runtime.voiceflow.com',
  versionID: 'production',
  assistant: {
    position: 'right',           // 'right' or 'left'
    sideSpacing: 20,             // Distance from side (in pixels)
    bottomSpacing: 20,           // Distance from bottom (in pixels)
    launcher: {
      type: 'icon',              // 'icon', 'text', or 'iconWithText'
      text: 'Chat with CatBot'   // Custom button text
    }
  }
});
```

### Advanced Customization
For more extensive customization options (available on paid Voiceflow plans):

```javascript
window.voiceflow.chat.load({
  verify: { projectID: 'YOUR_PROJECT_ID' },
  url: 'https://general-runtime.voiceflow.com',
  versionID: 'production',
  assistant: {
    // Basic positioning
    position: 'right',
    sideSpacing: 20,
    bottomSpacing: 20,
    
    // Appearance
    fonts: {
      family: 'inherit'  // Use 'inherit' or specify a Google font
    },
    colors: {
      primary: '#4CAF50'  // Your brand color
    },
    
    // Header appearance
    header: {
      text: 'CatBot',
      description: 'I can help you adopt a cat or answer questions about Cat Connection'
    },
    
    // Launcher appearance
    launcher: {
      type: 'iconWithText',
      text: 'Chat with CatBot'
    }
  }
});
```

## Troubleshooting

### Common Issues and Solutions

1. **Widget not appearing**:
   - Check that the JavaScript snippet is correctly placed in your HTML
   - Verify that your project ID is correct
   - Ensure there are no JavaScript errors on your page

2. **Responses not working correctly**:
   - Test the same flow in the Voiceflow designer
   - Check for updated content that might affect conversation flows
   - Verify that the correct version ID is being used

3. **Visual styling issues**:
   - Inspect for CSS conflicts with your website
   - Try adjusting the custom styling parameters
   - Consider using the 'inherit' font setting to match your site

### Getting Help

For technical issues:
- During the first year (managed hosting): Contact our support team
- Self-hosting: Refer to Voiceflow's documentation and support resources

## Support Resources

- **Voiceflow Documentation**: [docs.voiceflow.com](https://docs.voiceflow.com)
- **Voiceflow Community**: [community.voiceflow.com](https://community.voiceflow.com)
- **Video Tutorials**: [Voiceflow YouTube Channel](https://www.youtube.com/c/Voiceflow)

For the first year, you can also contact our team directly at [support@yourcompany.com] for assistance with CatBot.

---

## Appendix: Version Control Best Practices

When managing your CatBot, follow these version control best practices:

1. **Keep a change log**: Document all changes made to each version
2. **Use descriptive version names**: For example, "April2025-SeniorCatUpdate"
3. **Take backups**: Export a copy of your project before making significant changes
4. **Test thoroughly**: Verify all conversation paths before publishing to production
5. **Limit access**: Only allow authorized staff to publish production versions

By following these guidelines, you'll ensure that your CatBot continues to effectively serve Cat Connection's mission of connecting deserving cats with loving homes.
