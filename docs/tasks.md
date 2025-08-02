# Schedule Scoop - Project Restructure Tasks

<details>
<summary><strong>Phase 1: Project Cleanup & Analysis (4-6 hours)</strong></summary>

### Preserve and move core functionality (1-2 hours)
- [*] **Copy armory/carleton-timetables.js to src/timetable-extractor.js**
  <details>
  <summary>Details</summary>
  > **What**: Move the main timetable extraction logic to the proper src/ directory
  > **Why**: The core functionality is currently in the experimental armory folder, but it's the main feature we need to keep
  > **How**: Copy the file, update any import/require statements in other files to point to the new location
  </details>

- [*] **Update all references to point to new location**
  <details>
  <summary>Details</summary>
  > **What**: Find all files that import or reference the carleton-timetables.js file
  > **Why**: After moving the file, we need to update all the paths so the extension still works
  > **How**: Search for "carleton-timetables" in all files and update the paths to "timetable-extractor"
  </details>

- [ ] **Test that extraction still works after move**
  <details>
  <summary>Details</summary>
  > **What**: Verify the timetable export functionality still works correctly
  > **Why**: Moving files can break functionality if references aren't updated properly
  > **How**: Load the extension in Chrome and test the export feature on Carleton's website
  </details>

### Remove experimental features (1-2 hours)
- [ ] **Delete armory folder (reaction time, chimp test, xAI)**
  <details>
  <summary>Details</summary>
  > **What**: Remove the entire armory folder containing experimental tools
  > **Why**: These are not core to the main timetable export functionality and add unnecessary complexity
  > **How**: Delete the folder, but make sure we've moved the carleton-timetables.js first
  </details>

- [ ] **Remove unused dependencies and imports**
  <details>
  <summary>Details</summary>
  > **What**: Find and remove any import statements or dependencies that were only used by the experimental features
  > **Why**: Clean up the codebase and reduce bundle size
  > **How**: Search for imports that reference armory/ files and remove them
  </details>

- [ ] **Clean up manifest.json permissions**
  <details>
  <summary>Details</summary>
  > **What**: Review and remove unnecessary permissions from the Chrome extension manifest
  > **Why**: Only request permissions that are actually needed for the core functionality
  > **How**: Check each permission in manifest.json and remove any that were only used by experimental features
  </details>

- [ ] **Remove unused image assets**
  <details>
  <summary>Details</summary>
  > **What**: Delete image files that were only used by the experimental features
  > **Why**: Reduce extension size and clean up the project
  > **How**: Check which images are referenced in the deleted armory files and remove them
  </details>

### Audit current codebase (2-2 hours)
- [ ] **Map all file dependencies**
  <details>
  <summary>Details</summary>
  > **What**: Create a diagram or list showing which files import/require which other files
  > **Why**: Understand the current structure before making changes, so we don't break anything
  > **How**: Go through each file and list what it imports, create a dependency graph
  </details>

- [ ] **Identify duplicate functions**
  <details>
  <summary>Details</summary>
  > **What**: Find functions that do the same thing in different files
  > **Why**: Remove code duplication to make the codebase cleaner and easier to maintain
  > **How**: Search for similar function names and compare their implementations
  </details>

- [ ] **Document current tab management flow**
  <details>
  <summary>Details</summary>
  > **What**: Write down how the extension currently opens, manages, and closes tabs
  > **Why**: The current tab management is overly complex and we need to understand it to simplify it
  > **How**: Trace through the background.js file and document each tab operation
  </details>

- [ ] **List all console.log statements to remove**
  <details>
  <summary>Details</summary>
  > **What**: Find all console.log, console.error, and console.warn statements in the code
  > **Why**: Clean up debug code that shouldn't be in production
  > **How**: Search for "console." in all files and create a list to remove later
  </details>

</details>

<details>
<summary><strong>Phase 2: Implement Direct Page Injection (6-8 hours)</strong></summary>

### Remove popup-based architecture (2-3 hours)
- [ ] **Remove popup files and dependencies**
  <details>
  <summary>Details</summary>
  > **What**: Delete popup.html, popup-minimal.html, popup-clean.html and their associated JS files
  > **Why**: Switching to direct page injection eliminates the need for popup interfaces
  > **How**: Remove popup files and update manifest.json to remove popup references
  </details>

- [ ] **Update manifest.json for content script injection**
  <details>
  <summary>Details</summary>
  > **What**: Modify manifest.json to use content_scripts instead of action with popup
  > **Why**: Content scripts can inject directly into Carleton pages, eliminating popup complexity
  > **How**: Replace action/popup configuration with content_scripts that target Carleton domains
  </details>

- [ ] **Remove popup-related CSS files**
  <details>
  <summary>Details</summary>
  > **What**: Delete style.css, clean-style.css and other popup-specific styling
  > **Why**: No longer needed since we're not using popups
  > **How**: Remove CSS files and update any remaining references
  </details>

### Implement content script injection (3-4 hours)
- [ ] **Create content script for Carleton pages**
  <details>
  <summary>Details</summary>
  > **What**: Create a new content script that injects an export button directly onto Carleton timetable pages
  > **Why**: Users can see and click the export button right where they need it, without opening a popup
  > **How**: Create content script that detects Carleton timetable pages and injects a styled export button
  </details>

- [ ] **Design inline export button UI**
  <details>
  <summary>Details</summary>
  > **What**: Create a clean, contextual export button that appears on the Carleton timetable page
  > **Why**: The button should look native to the page and be easily discoverable
  > **How**: Design a button that matches Carleton's UI style and position it prominently on the page
  </details>

- [ ] **Implement button click handling**
  <details>
  <summary>Details</summary>
  > **What**: Handle the export button click to start the timetable extraction process
  > **Why**: Users click the button to begin the export process
  > **How**: Add click event listener to the injected button that triggers the extraction logic
  </details>

- [ ] **Add loading states and feedback**
  <details>
  <summary>Details</summary>
  > **What**: Show loading indicators and progress feedback directly on the page
  > **Why**: Users need to know the export is working and what step it's on
  > **How**: Display progress messages and loading spinners near the export button
  </details>

### Simplify background script (1-2 hours)
- [ ] **Remove complex tab management**
  <details>
  <summary>Details</summary>
  > **What**: Eliminate the complex tab tracking and management system from background.js
  > **Why**: With direct page injection, we don't need to create/manage multiple tabs
  > **How**: Remove tab creation, tracking, and cleanup code from background.js
  </details>

- [ ] **Simplify message passing**
  <details>
  <summary>Details</summary>
  > **What**: Reduce message complexity between content script and background script
  > **Why**: Direct page injection simplifies the communication flow
  > **How**: Consolidate messages to just handle export requests and file downloads
  </details>

</details>

<details>
<summary><strong>Phase 3: Core Functionality Refactor (8-12 hours)</strong></summary>

### Modularize timetable logic (5-7 hours)
- [ ] **Break down carleton-timetables.js into smaller, focused functions**
  <details>
  <summary>Details</summary>
  > **What**: Split the large 971-line file into smaller, more manageable functions
  > **Why**: The current file is too large and does too many things, making it hard to understand and maintain
  > **How**: Identify logical sections (navigation, extraction, calendar generation) and split them into separate functions
  </details>

- [ ] **Create TimetableExtractor class**
  <details>
  <summary>Details</summary>
  > **What**: Create a class that handles all the timetable extraction logic
  > **Why**: Encapsulate the extraction logic and make it more organized and testable
  > **How**: Move extraction functions into a class with methods like extract(), navigate(), parseCourses()
  </details>

- [ ] **Create CalendarGenerator class**
  <details>
  <summary>Details</summary>
  > **What**: Create a class that handles ICS calendar file generation
  > **Why**: Separate calendar generation from extraction logic for better organization
  > **How**: Move calendar-related functions into a class with methods like generateICS(), formatEvent(), etc.
  </details>

- [ ] **Add proper error handling**
  <details>
  <summary>Details</summary>
  > **What**: Add try-catch blocks and proper error messages throughout the extraction process
  > **Why**: Currently the extension can fail silently or with unclear error messages
  > **How**: Wrap each major operation in try-catch and provide user-friendly error messages
  </details>

### Improve state management (3-5 hours)
- [ ] **Replace complex session storage with simple state machine**
  <details>
  <summary>Details</summary>
  > **What**: Replace the complex session storage system with a simple state machine
  > **Why**: Current state management is hard to follow and error-prone
  > **How**: Create a simple state enum (IDLE, EXTRACTING, COMPLETE, ERROR) and manage transitions
  </details>

- [ ] **Implement proper loading states**
  <details>
  <summary>Details</summary>
  > **What**: Add visual feedback when the extension is working
  > **Why**: Users need to know the extension is working and not frozen
  > **How**: Show loading spinners, progress bars, or status messages during extraction
  </details>

- [ ] **Add progress indicators**
  <details>
  <summary>Details</summary>
  > **What**: Show step-by-step progress of the extraction process
  > **Why**: Users want to know what step the extension is on
  > **How**: Display progress like "Logging in...", "Extracting courses...", "Generating calendar..."
  </details>

- [ ] **Handle edge cases (no courses, network errors, etc.)**
  <details>
  <summary>Details</summary>
  > **What**: Add handling for scenarios like no courses enrolled, network failures, or invalid data
  > **Why**: The extension should gracefully handle all possible scenarios
  > **How**: Add checks for empty course lists, network timeouts, and provide helpful error messages
  </details>

</details>

<details>
<summary><strong>Phase 4: User Interface Overhaul (6-10 hours)</strong></summary>

### Design contextual page UI (3-5 hours)
- [ ] **Create inline export button design**
  <details>
  <summary>Details</summary>
  > **What**: Design a clean, contextual export button that appears on Carleton timetable pages
  > **Why**: The button should look native to the page and be easily discoverable
  > **How**: Create a button that matches Carleton's UI style and position it prominently
  </details>

- [ ] **Add clear progress indicators on page**
  <details>
  <summary>Details</summary>
  > **What**: Show users exactly what step the extension is on during extraction
  > **Why**: Users need feedback to know the extension is working
  > **How**: Display step-by-step progress like "Step 1/4: Logging in..." directly on the page
  </details>

- [ ] **Implement proper error messaging on page**
  <details>
  <summary>Details</summary>
  > **What**: Show user-friendly error messages when something goes wrong
  > **Why**: Current error messages are technical and confusing
  > **How**: Create simple, actionable error messages like "Please log in to Carleton first"
  </details>

- [ ] **Add success confirmation on page**
  <details>
  <summary>Details</summary>
  > **What**: Show a clear success message when export completes
  > **Why**: Users need to know the export worked
  > **How**: Display a success message with download link or confirmation directly on the page
  </details>

- [ ] **Make UI responsive and accessible**
  <details>
  <summary>Details</summary>
  > **What**: Ensure the injected UI looks good and is accessible on different screen sizes
  > **Why**: Users have different monitor sizes and accessibility needs
  > **How**: Use CSS flexbox/grid, add ARIA labels, and test on different window sizes
  </details>

### Improve user experience (3-5 hours)
- [ ] **Add loading animations**
  <details>
  <summary>Details</summary>
  > **What**: Add visual animations like spinners or progress bars during extraction
  > **Why**: Makes the extension feel more polished and responsive
  > **How**: Use CSS animations or simple loading spinners during long operations
  </details>

- [ ] **Implement one-click export**
  <details>
  <summary>Details</summary>
  > **What**: Make the export process as simple as possible - just one button click
  > **Why**: Current process requires multiple steps and configuration
  > **How**: Automatically detect the current term and start extraction with one click
  </details>

- [ ] **Add export history (local only)**
  <details>
  <summary>Details</summary>
  > **What**: Keep a local record of previous exports for user reference
  > **Why**: Users might want to see when they last exported their schedule
  > **How**: Store export timestamps and course counts locally in Chrome storage
  </details>

- [ ] **Create settings panel for term selection**
  <details>
  <summary>Details</summary>
  > **What**: Add a simple settings area where users can choose which term to export
  > **Why**: Sometimes users want to export a different term than the current one
  > **How**: Add a collapsible settings section with term/year dropdowns
  </details>

</details>

<details>
<summary><strong>Phase 5: Code Quality & Modernization (4-6 hours)</strong></summary>

### Modernize JavaScript (2-3 hours)
- [ ] **Convert to ES6+ syntax**
  <details>
  <summary>Details</summary>
  > **What**: Update code to use modern JavaScript features like const/let, arrow functions, template literals
  > **Why**: Makes code more readable and maintainable
  > **How**: Replace var with const/let, convert functions to arrow functions where appropriate
  </details>

- [ ] **Use async/await instead of callbacks**
  <details>
  <summary>Details</summary>
  > **What**: Replace callback-based code with async/await for better readability
  > **Why**: Async/await is easier to read and debug than nested callbacks
  > **How**: Convert functions that use callbacks to use async/await instead
  </details>

- [ ] **Implement proper error handling**
  <details>
  <summary>Details</summary>
  > **What**: Add comprehensive error handling throughout the codebase
  > **Why**: Currently errors can cause the extension to fail silently
  > **How**: Add try-catch blocks and proper error logging
  </details>

- [ ] **Add TypeScript definitions (optional)**
  <details>
  <summary>Details</summary>
  > **What**: Add TypeScript type definitions to make the code more robust
  > **Why**: TypeScript helps catch errors at compile time
  > **How**: Add .d.ts files or convert to TypeScript if the team wants to
  </details>

### Clean up code (2-3 hours)
- [ ] **Remove all console.log statements**
  <details>
  <summary>Details</summary>
  > **What**: Remove all debug console.log, console.error, and console.warn statements
  > **Why**: Debug code shouldn't be in production and clutters the console
  > **How**: Search for all console statements and remove them, or replace with proper logging
  </details>

- [ ] **Add proper JSDoc comments**
  <details>
  <summary>Details</summary>
  > **What**: Add documentation comments to all functions explaining what they do
  > **Why**: Makes the code easier to understand for new developers
  > **How**: Add /** */ comments above each function describing parameters, return values, and purpose
  </details>

- [ ] **Implement consistent naming conventions**
  <details>
  <summary>Details</summary>
  > **What**: Ensure all variables, functions, and files follow consistent naming patterns
  > **Why**: Makes code more readable and professional
  > **How**: Use camelCase for variables/functions, PascalCase for classes, kebab-case for files
  </details>

- [ ] **Add input validation**
  <details>
  <summary>Details</summary>
  > **What**: Add checks to ensure data is valid before processing it
  > **Why**: Prevents crashes and unexpected behavior from invalid data
  > **How**: Add checks for null/undefined values, validate data types, and handle edge cases
  </details>

</details>

<details>
<summary><strong>Phase 6: Testing & Validation (3-5 hours)</strong></summary>

### Test core functionality (2-3 hours)
- [ ] **Test timetable extraction on Carleton site**
  <details>
  <summary>Details</summary>
  > **What**: Test the extension on the actual Carleton University website
  > **Why**: Need to ensure it works with the real website, not just in isolation
  > **How**: Load the extension in Chrome, go to Carleton's site, and test the export feature
  </details>

- [ ] **Validate ICS file generation**
  <details>
  <summary>Details</summary>
  > **What**: Check that the generated ICS calendar files are valid and can be imported
  > **Why**: The ICS file needs to work with calendar applications like Google Calendar
  > **How**: Generate an ICS file and try importing it into Google Calendar or other calendar apps
  </details>

- [ ] **Test calendar import functionality**
  <details>
  <summary>Details</summary>
  > **What**: Test the direct calendar integration features
  > **Why**: Users should be able to directly add courses to their calendar
  > **How**: Test the "Add to Google Calendar" and other calendar integration features
  </details>

- [ ] **Verify term detection logic**
  <details>
  <summary>Details</summary>
  > **What**: Test that the extension correctly detects the current academic term
  > **Why**: Users need the correct term to be selected automatically
  > **How**: Test during different times of year to ensure term detection works correctly
  </details>

### Error handling tests (1-2 hours)
- [ ] **Test with no courses enrolled**
  <details>
  <summary>Details</summary>
  > **What**: Test what happens when a user has no courses enrolled for the selected term
  > **Why**: Need to handle this edge case gracefully
  > **How**: Create a test scenario where no courses are found and verify proper error message
  </details>

- [ ] **Test with network failures**
  <details>
  <summary>Details</summary>
  > **What**: Test how the extension behaves when the Carleton website is slow or unavailable
  > **Why**: Network issues can cause the extension to fail
  > **How**: Simulate slow network or disconnect and test error handling
  </details>

- [ ] **Test with invalid term selection**
  <details>
  <summary>Details</summary>
  > **What**: Test what happens when an invalid term is selected
  > **Why**: Users might accidentally select invalid terms
  > **How**: Try to export with invalid term/year combinations and verify error handling
  </details>

- [ ] **Test with different browsers**
  <details>
  <summary>Details</summary>
  > **What**: Test the extension in different browsers (Chrome, Edge, etc.)
  > **Why**: Chrome extensions should work in Chromium-based browsers
  > **How**: Install the extension in different browsers and test functionality
  </details>

</details>

<details>
<summary><strong>Phase 7: Documentation & Deployment (2-4 hours)</strong></summary>

### Update documentation (1-2 hours)
- [ ] **Rewrite README.md with new structure**
  <details>
  <summary>Details</summary>
  > **What**: Update the README to reflect the new simplified project structure
  > **Why**: Users and developers need accurate documentation
  > **How**: Rewrite the README with new file structure, features, and installation steps
  </details>

- [ ] **Add installation instructions**
  <details>
  <summary>Details</summary>
  > **What**: Create clear step-by-step installation instructions
  > **Why**: Users need to know how to install the extension
  > **How**: Add instructions for both Chrome Web Store and manual installation
  </details>

- [ ] **Document API/function usage**
  <details>
  <summary>Details</summary>
  > **What**: Document how to use the main functions and classes
  > **Why**: Future developers need to understand how the code works
  > **How**: Add JSDoc comments and create API documentation
  </details>

- [ ] **Create user guide**
  <details>
  <summary>Details</summary>
  > **What**: Create a simple guide for end users
  > **Why**: Users need to know how to use the extension
  > **How**: Create a simple guide with screenshots and step-by-step instructions
  </details>

### Prepare for deployment (1-2 hours)
- [ ] **Update manifest.json version**
  <details>
  <summary>Details</summary>
  > **What**: Increment the version number in manifest.json
  > **Why**: Chrome Web Store requires version updates for new releases
  > **How**: Update the version field in manifest.json (e.g., from 2.0.0 to 2.1.0)
  </details>

- [ ] **Test in Chrome Web Store**
  <details>
  <summary>Details</summary>
  > **What**: Test the extension as it would appear in the Chrome Web Store
  > **Why**: Ensure the extension works properly when installed from the store
  > **How**: Package the extension and test installation from a .crx file
  </details>

- [ ] **Create release notes**
  <details>
  <summary>Details</summary>
  > **What**: Document what changes were made in this version
  > **Why**: Users need to know what's new or fixed
  > **How**: Create a CHANGELOG.md or update release notes with key changes
  </details>

- [ ] **Update privacy policy**
  <details>
  <summary>Details</summary>
  > **What**: Review and update the privacy policy if needed
  > **Why**: Privacy policy should reflect current data handling practices
  > **How**: Review what data the extension collects and update policy accordingly
  </details>

</details>

<details>
<summary><strong>Phase 8: Optional Enhancements (4-8 hours)</strong></summary>

### Performance optimizations (2-4 hours)
- [ ] **Minimize bundle size**
  <details>
  <summary>Details</summary>
  > **What**: Reduce the total size of the extension files
  > **Why**: Smaller extensions load faster and use less memory
  > **How**: Remove unused code, minify JavaScript/CSS, optimize images
  </details>

- [ ] **Optimize DOM queries**
  <details>
  <summary>Details</summary>
  > **What**: Make DOM element selection more efficient
  > **Why**: Faster DOM queries improve extension performance
  > **How**: Cache DOM elements, use more specific selectors, avoid repeated queries
  </details>

- [ ] **Implement caching where appropriate**
  <details>
  <summary>Details</summary>
  > **What**: Cache frequently accessed data to avoid repeated operations
  > **Why**: Caching can significantly improve performance
  > **How**: Cache term data, user preferences, and other frequently accessed information
  </details>

### Additional features (2-4 hours)
- [ ] **Add support for other universities (if needed)**
  <details>
  <summary>Details</summary>
  > **What**: Extend the extension to work with other university websites
  > **Why**: Could expand the user base beyond Carleton University
  > **How**: Create modular extractors for different university systems
  </details>

- [ ] **Implement batch export for multiple terms**
  <details>
  <summary>Details</summary>
  > **What**: Allow users to export multiple terms at once
  > **Why**: Some users want their entire academic schedule
  > **How**: Add checkboxes for multiple terms and generate combined ICS file
  </details>

- [ ] **Add export format options (CSV, JSON)**
  <details>
  <summary>Details</summary>
  > **What**: Allow users to export in different formats besides ICS
  > **Why**: Different users have different needs (spreadsheets, data analysis)
  > **How**: Add format selection and create converters for CSV/JSON output
  </details>

</details>

<details>
<summary><strong>Technical Debt Items (2-3 hours)</strong></summary>

### Security improvements (1-2 hours)
- [ ] **Audit permissions in manifest.json**
  <details>
  <summary>Details</summary>
  > **What**: Review all permissions requested by the extension
  > **Why**: Only request permissions that are actually needed for security
  > **How**: Check each permission and remove any that aren't essential
  </details>

- [ ] **Implement Content Security Policy**
  <details>
  <summary>Details</summary>
  > **What**: Add CSP headers to prevent XSS attacks
  > **Why**: Improves security by restricting what scripts can run
  > **How**: Add appropriate CSP headers in manifest.json
  </details>

- [ ] **Validate all user inputs**
  <details>
  <summary>Details</summary>
  > **What**: Add validation for any data entered by users
  > **Why**: Prevents security vulnerabilities from malicious input
  > **How**: Add input validation for settings, term selection, etc.
  </details>

### Accessibility (1-1 hours)
- [ ] **Add ARIA labels**
  <details>
  <summary>Details</summary>
  > **What**: Add accessibility labels to UI elements
  > **Why**: Makes the extension usable by people with disabilities
  > **How**: Add aria-label attributes to buttons, inputs, and other interactive elements
  </details>

- [ ] **Ensure keyboard navigation**
  <details>
  <summary>Details</summary>
  > **What**: Make sure all functionality can be accessed via keyboard
  > **Why**: Some users rely on keyboard navigation
  > **How**: Test tab order and ensure all buttons/links are keyboard accessible
  </details>

- [ ] **Test with screen readers**
  <details>
  <summary>Details</summary>
  > **What**: Test the extension with screen reader software
  > **Why**: Ensures accessibility for visually impaired users
  > **How**: Use Chrome's built-in screen reader or test with actual screen reader software
  </details>

</details>

## Success Criteria
- [ ] Extension works with single click directly on Carleton pages
- [ ] No popup interface needed
- [ ] No complex tab management
- [ ] Clean, maintainable codebase
- [ ] Proper error handling
- [ ] User-friendly interface that appears contextually
- [ ] Reliable timetable extraction
- [ ] Privacy-first approach maintained

## Notes for Collaboration
- Use feature branches for each phase
- Regular code reviews between team members
- Test each phase before moving to next
- Keep communication open about progress
- Document any decisions or changes made 