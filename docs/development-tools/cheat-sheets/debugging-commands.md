# Debugging Commands Cheat Sheet

Quick reference for debugging web applications in browsers, terminals, and development tools.

## Chrome DevTools Shortcuts

### Opening DevTools
```
Windows/Linux          Mac
F12                    Cmd + Opt + I
Ctrl + Shift + I       Cmd + Opt + I
Ctrl + Shift + C       Cmd + Opt + C (Inspect element)
Ctrl + Shift + J       Cmd + Opt + J (Console)
```

### Navigation
```
Windows/Linux          Mac                     Action
Ctrl + [               Cmd + [                 Previous panel
Ctrl + ]               Cmd + ]                 Next panel
Ctrl + Shift + P       Cmd + Shift + P         Command palette
Ctrl + Shift + D       Cmd + Shift + D         Toggle device toolbar
Ctrl + Shift + M       Cmd + Shift + M         Toggle mobile view
Esc                    Esc                     Toggle drawer
Ctrl + L               Cmd + K                 Clear console
```

### Elements Panel
```
Windows/Linux          Mac                     Action
Arrow keys             Arrow keys              Navigate DOM
Enter                  Enter                   Edit attribute
H                      H                       Hide element
Delete                 Delete                  Delete element
Ctrl + Z               Cmd + Z                 Undo change
F2                     F2                      Edit as HTML
Ctrl + F               Cmd + F                 Search DOM
```

### Console
```
Windows/Linux          Mac                     Action
Ctrl + L               Cmd + K                 Clear console
↑/↓                    ↑/↓                     Previous/next command
Ctrl + U               Cmd + U                 Clear current command
Tab                    Tab                     Autocomplete
Shift + Enter          Shift + Enter           Multi-line input
```

### Sources/Debugger
```
Windows/Linux          Mac                     Action
Ctrl + O               Cmd + O                 Open file
Ctrl + Shift + O       Cmd + Shift + O         Go to symbol
Ctrl + G               Cmd + L                 Go to line
Ctrl + P               Cmd + P                 Go to file
F8                     F8                      Resume/pause
F9                     F9                      Toggle breakpoint
F10                    F10                     Step over
F11                    F11                     Step into
Shift + F11            Shift + F11             Step out
Ctrl + Shift + E       Cmd + Shift + E         Run snippet
```

### Network Panel
```
Windows/Linux          Mac                     Action
Ctrl + E               Cmd + E                 Start/stop recording
Ctrl + F               Cmd + F                 Search requests
Ctrl + R               Cmd + R                 Reload (normal)
Ctrl + Shift + R       Cmd + Shift + R         Hard reload (clear cache)
Hold Shift + reload    Hold Shift + reload     Empty cache & hard reload
```

### Performance Panel
```
Windows/Linux          Mac                     Action
Ctrl + E               Cmd + E                 Start/stop recording
Ctrl + Shift + E       Cmd + Shift + E         Record page load
```

## Chrome DevTools Console Commands

### Selection
```javascript
// Select element by ID
$('#myId')              // Same as document.getElementById('myId')

// Select element by selector
$('.myClass')           // First matching element
$$('.myClass')          // All matching elements (array)

// Currently selected element in Elements panel
$0                      // Currently selected
$1                      // Previously selected
$2                      // Second previously selected

// Example:
$0.style.background = 'red'  // Change selected element background
```

### Inspection
```javascript
// Inspect element
inspect($('.myClass'))  // Opens Elements panel for element

// Get event listeners
getEventListeners($0)   // All listeners on selected element

// Monitor events
monitorEvents($0)       // Log all events
monitorEvents($0, ['click', 'mouseenter'])  // Log specific events
unmonitorEvents($0)     // Stop monitoring

// Copy to clipboard
copy($0)                // Copy selected element
copy(object)            // Copy any object as JSON
```

### Performance
```javascript
// Measure execution time
console.time('myOperation')
// ... code to measure
console.timeEnd('myOperation')

// Profile CPU
console.profile('myProfile')
// ... code to profile
console.profileEnd('myProfile')

// Memory usage
console.memory.usedJSHeapSize

// Performance marks
performance.mark('start')
// ... code
performance.mark('end')
performance.measure('myMeasure', 'start', 'end')
console.log(performance.getEntriesByType('measure'))
```

### Console Output
```javascript
// Different log levels
console.log('Info')
console.info('Info')
console.warn('Warning')
console.error('Error')
console.debug('Debug')

// Styled output
console.log('%cStyled text', 'color: red; font-size: 20px')
console.log('%cRed %cBlue', 'color: red', 'color: blue')

// Tables
console.table([{a: 1, b: 2}, {a: 3, b: 4}])

// Groups
console.group('Group')
console.log('Item 1')
console.log('Item 2')
console.groupEnd()

// Collapsible groups
console.groupCollapsed('Hidden Group')
console.log('Hidden by default')
console.groupEnd()

// Counts
console.count('myCounter')  // Increments each time
console.countReset('myCounter')  // Reset counter

// Assertions
console.assert(1 === 2, 'This will show error')
console.assert(1 === 1, 'This will not show')

// Stack trace
console.trace('Stack trace here')

// Clear
console.clear()
```

### Debugging
```javascript
// Debugger statement
debugger;  // Pauses execution

// Break on property access
Object.defineProperty(window, 'myVar', {
  get() { debugger; return this._myVar; },
  set(value) { debugger; this._myVar = value; }
})

// Break on function call
debug(functionName)     // Breaks when function is called
undebug(functionName)   // Remove debug

// Monitor function calls
monitor(functionName)   // Logs when function is called
unmonitor(functionName) // Stop monitoring
```

## Terminal Debugging

### Node.js Debugging

```bash
# Run with inspector
node --inspect app.js

# Run and break on first line
node --inspect-brk app.js

# Run with debugger on specific port
node --inspect=9229 app.js

# Debug with chrome://inspect
# 1. Run: node --inspect app.js
# 2. Open Chrome: chrome://inspect
# 3. Click "Open dedicated DevTools for Node"
```

### NPM/Node Debugging

```bash
# Show npm debug logs
npm run dev --verbose

# Show even more debug info
npm run dev --loglevel=verbose

# Debug npm scripts
DEBUG=* npm run dev

# Check Node.js version
node --version

# Check npm version
npm --version

# Clear npm cache
npm cache clean --force

# Reinstall node_modules
rm -rf node_modules package-lock.json
npm install
```

### Astro Debugging

```bash
# Dev mode (shows errors)
npm run dev

# Build with debug output
npm run build -- --verbose

# Preview build locally
npm run preview

# Check for Astro errors
npx astro check

# Astro info (versions, config)
npx astro info

# Clear Astro cache
rm -rf .astro node_modules/.astro
```

## Network Inspection

### Chrome DevTools Network Tab

**Filter requests:**
```
Toolbar → Filter box

Examples:
domain:example.com          # Requests to specific domain
status-code:404             # By status code
method:POST                 # By HTTP method
mime-type:image/png         # By MIME type
larger-than:1k              # By size
-method:OPTIONS             # Exclude OPTIONS requests
```

**Request details:**
- **Headers tab** - Request/response headers
- **Preview tab** - Formatted response
- **Response tab** - Raw response
- **Timing tab** - Request timing breakdown
- **Cookies tab** - Cookies sent/received

**Copy as cURL:**
```
Right-click request → Copy → Copy as cURL

# Paste in terminal to replay request
curl 'https://api.example.com/data' \
  -H 'Authorization: Bearer token' \
  -H 'Content-Type: application/json'
```

**Copy as Fetch:**
```
Right-click request → Copy → Copy as fetch

# Paste in console to replay as JavaScript
fetch('https://api.example.com/data', {
  headers: { 'Authorization': 'Bearer token' }
})
```

**Throttle network:**
```
Toolbar → No throttling dropdown
Options: Fast 3G, Slow 3G, Offline, Custom
```

**Block requests:**
```
Right-click request → Block request URL
Right-click request → Block request domain
```

### cURL Debugging

```bash
# Simple GET request
curl https://api.example.com/data

# GET with headers
curl -H "Authorization: Bearer token" \
     https://api.example.com/data

# POST with JSON body
curl -X POST https://api.example.com/data \
     -H "Content-Type: application/json" \
     -d '{"key": "value"}'

# POST with form data
curl -X POST https://api.example.com/data \
     -d "name=John" \
     -d "email=john@example.com"

# Show response headers
curl -i https://api.example.com/data

# Show only headers
curl -I https://api.example.com/data

# Follow redirects
curl -L https://api.example.com/data

# Verbose (show full request/response)
curl -v https://api.example.com/data

# Save response to file
curl https://api.example.com/data -o output.json

# Show timing info
curl -w "@curl-timing.txt" https://api.example.com/data

# curl-timing.txt contents:
# time_total: %{time_total}\n

# Upload file
curl -X POST https://api.example.com/upload \
     -F "file=@/path/to/file.jpg"

# Test with different user agents
curl -A "Mozilla/5.0" https://api.example.com/data
```

### HTTPie (Better than cURL)

```bash
# Install
npm install -g httpie

# GET request
http GET https://api.example.com/data

# POST JSON
http POST https://api.example.com/data key=value

# POST with headers
http POST https://api.example.com/data \
     Authorization:"Bearer token" \
     key=value

# Download file
http --download https://example.com/file.pdf

# Follow redirects
http --follow https://example.com/redirect

# Verbose
http --verbose GET https://api.example.com/data
```

## Performance Profiling

### Chrome DevTools Performance Tab

**Record performance:**
```
1. Open Performance tab
2. Click record button (●)
3. Interact with page
4. Click stop button (■)
5. Analyze results
```

**What to look for:**
- **Red triangles** - Long tasks (> 50ms)
- **Yellow sections** - JavaScript execution
- **Purple sections** - Rendering/painting
- **Green sections** - Painting
- **Gray sections** - Idle time

**FPS meter:**
```
1. Cmd/Ctrl + Shift + P
2. Type "Show frames per second (FPS) meter"
3. See real-time FPS while interacting
```

**Performance monitor:**
```
1. Cmd/Ctrl + Shift + P
2. Type "Show Performance monitor"
3. See real-time metrics:
   - CPU usage
   - JS heap size
   - DOM nodes
   - JS event listeners
   - Layouts per second
```

### Lighthouse

```bash
# Run Lighthouse from DevTools
1. Open DevTools
2. Click "Lighthouse" tab
3. Select categories
4. Click "Analyze page load"

# Run from command line
npm install -g lighthouse
lighthouse https://example.com
lighthouse https://example.com --view  # Open report

# Run in CI
npm install -g @lhci/cli
lhci autorun
```

### Chrome DevTools Coverage

**Find unused CSS/JS:**
```
1. Cmd/Ctrl + Shift + P
2. Type "Show Coverage"
3. Click reload button
4. See unused code (red bars)
5. Click file to see unused lines
```

**Interpret results:**
- Red bars = unused code
- Green bars = used code
- Goal: 80%+ green

## Memory Debugging

### Chrome DevTools Memory Tab

**Take heap snapshot:**
```
1. Open Memory tab
2. Select "Heap snapshot"
3. Click "Take snapshot"
4. Analyze objects in memory
```

**Compare snapshots:**
```
1. Take snapshot 1
2. Interact with page
3. Take snapshot 2
4. Compare to find leaks
```

**Allocation timeline:**
```
1. Open Memory tab
2. Select "Allocation instrumentation on timeline"
3. Click record
4. Interact with page
5. Stop recording
6. See allocations over time
```

**What to look for:**
- **Detached DOM nodes** - Memory leak
- **Growing heap size** - Possible leak
- **Event listeners** - May prevent GC

## Mobile Debugging

### Chrome Remote Debugging (Android)

```
1. Enable USB debugging on Android
2. Connect phone via USB
3. Open chrome://inspect in Chrome
4. Click "inspect" on your device
5. Debug as normal
```

### iOS Safari Debugging

```
1. Enable Web Inspector on iOS:
   Settings → Safari → Advanced → Web Inspector

2. Connect iPhone via USB

3. Open Safari on Mac:
   Develop → [Your iPhone] → [Page]

4. Debug as normal
```

### Responsive Mode

```
Chrome DevTools:
Cmd/Ctrl + Shift + M    # Toggle device toolbar

Options:
- Select device preset
- Set custom dimensions
- Rotate device
- Throttle network
- Show media queries
- Show rulers
```

## Layout Debugging

### Visualize Layout Issues

```javascript
// Show all element outlines
[].forEach.call(
  document.querySelectorAll('*'),
  el => el.style.outline = '1px solid red'
)

// Show elements with specific property
[].forEach.call(
  document.querySelectorAll('*'),
  el => {
    if (getComputedStyle(el).position === 'absolute') {
      el.style.outline = '2px solid blue'
    }
  }
)
```

### Chrome Layout Shift Regions

```
1. Open DevTools
2. Cmd/Ctrl + Shift + P
3. Type "Show Layout Shift Regions"
4. Reload page
5. See blue rectangles where shifts occur
```

### Chrome Layer Borders

```
1. Open DevTools
2. Cmd/Ctrl + Shift + P
3. Type "Show layer borders"
4. See what's being composited
```

### Force Element State

```
Chrome DevTools Elements panel:
1. Select element
2. Right-click
3. Force state → :hover/:active/:focus/:visited
```

## Debugging Tips

### Break on DOM Changes

```
Chrome DevTools Elements panel:
1. Right-click element
2. Break on...
   - Subtree modifications
   - Attribute modifications
   - Node removal
```

### XHR/Fetch Breakpoints

```
Chrome DevTools Sources panel:
1. Expand "XHR/fetch Breakpoints"
2. Click + to add URL pattern
3. Debugger breaks on matching requests
```

### Event Listener Breakpoints

```
Chrome DevTools Sources panel:
1. Expand "Event Listener Breakpoints"
2. Check events to break on:
   - Mouse → click
   - Keyboard → keydown
   - Form → submit
   - Etc.
```

### Conditional Breakpoints

```
Chrome DevTools Sources panel:
1. Right-click line number
2. "Add conditional breakpoint"
3. Enter condition (e.g., "userId === 123")
4. Breaks only when condition is true
```

### Logpoints (Non-Breaking Breakpoints)

```
Chrome DevTools Sources panel:
1. Right-click line number
2. "Add logpoint"
3. Enter message (e.g., "User ID: {userId}")
4. Logs without breaking
```

## Quick Debugging Checklist

### Page Not Loading
```
☐ Check console for errors
☐ Check network tab for failed requests
☐ Check if JavaScript is enabled
☐ Check if ad blocker is interfering
☐ Hard reload (Ctrl+Shift+R / Cmd+Shift+R)
☐ Check CORS errors
☐ Check if API is running
```

### Styling Issues
```
☐ Inspect element
☐ Check computed styles
☐ Check if CSS loaded (Network tab)
☐ Check CSS specificity (DevTools shows)
☐ Check inherited styles
☐ Check :hover/:focus states
☐ Check mobile/responsive view
☐ Clear browser cache
```

### JavaScript Errors
```
☐ Check console for error message
☐ Check stack trace
☐ Add console.log() statements
☐ Add breakpoints
☐ Check if variables are defined
☐ Check function arguments
☐ Check async/await usage
☐ Check promise rejections
```

### Performance Issues
```
☐ Run Lighthouse audit
☐ Check Performance tab
☐ Check Network tab (waterfall)
☐ Check Coverage tab (unused code)
☐ Check for layout shifts
☐ Check for long tasks (> 50ms)
☐ Check image sizes
☐ Check JavaScript bundle size
```

### Network Issues
```
☐ Check Network tab for failed requests
☐ Check request/response headers
☐ Check request payload
☐ Check response status code
☐ Check CORS headers
☐ Check if API endpoint is correct
☐ Test request with cURL
☐ Check network throttling
```

---

**Pro Tips:**
- Use `debugger;` statement when console.log isn't enough
- Use Chrome DevTools → Sources → "Pause on exceptions"
- Record everything with Performance tab when investigating slowness
- Use Coverage tab to find unused CSS/JS
- Use Network tab → "Block request URL" to test fallbacks
- Mobile debug via chrome://inspect (Android) or Safari Develop menu (iOS)
