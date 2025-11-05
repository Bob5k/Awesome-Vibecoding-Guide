# Glossary 📖

A comprehensive reference guide for all technical terms, concepts, and acronyms used throughout the Awesome Vibecoding Guide. Terms are organized by category and alphabetized within each section for easy navigation.

---

## Core Vibecoding Concepts

**Act Mode**: A development mode where the AI agent executes a pre-written plan, implementing tasks step-by-step based on specifications saved in markdown files.

**BYOK (Bring Your Own Key)**: An approach where developers use their own API keys from AI providers instead of paying for bundled services, allowing for greater cost control and flexibility.

**Cascade**: Windsurf's AI agent that helps with coding tasks by referencing documentation and workflows automatically.

**Context Compression**: The process of summarizing or condensing conversation history to free up space in an AI model's context window while preserving essential information.

**Context Debt**: The accumulation of unnecessary or outdated information in a conversation that degrades AI performance over time, similar to technical debt in software development.

**Context Window**: The maximum amount of text (measured in tokens) that an AI model can consider and remember in a single conversation or interaction.

**Dialog Compression**: See **Context Compression**.

**Markdown Memory Pattern**: A workflow strategy where important information is saved to .md files instead of kept in conversation, reducing context usage and providing persistent knowledge storage.

**Plan Mode**: A development mode where you discuss and create a comprehensive project plan with the AI before any code is written, often saving the plan to a markdown file.

**Spec-Driven Development**: An approach where you create detailed specifications and plans before coding, allowing AI agents to implement features more accurately and consistently.

**The 60-85% Rule**: A context management guideline suggesting optimal AI performance occurs when using 60-85% of the context window; going beyond 85% can degrade response quality.

**Vibecoder**: A developer who uses AI assistants as collaborative partners in software development, emphasizing efficient workflows and cost-effective tool combinations.

**Vibecoding**: An approach to software development where you collaborate with AI as a coding partner, using natural language and structured workflows to build applications efficiently.

---

## Development Tools & Software

**AmpCode**: An alternative AI coding assistant CLI tool with a free tier, offering MCP server support and active development.

**Claude Code**: Anthropic's official CLI tool for AI-assisted coding, integrated with Claude's language model capabilities.

**CLI (Command-Line Interface)**: A text-based interface where you type commands to interact with software, as opposed to clicking buttons in a graphical interface.

**Cursor**: An AI-powered code editor (IDE) with built-in AI assistance and support for external AI models.

**Droid CLI**: A command-line coding agent with autonomous planning capabilities, permission management, and Bring Your Own Key support.

**Gemini CLI**: Google's command-line interface for accessing Gemini AI models, offering a generous free tier for development work.

**Git**: A version control system that tracks changes to your code over time, allowing you to save versions, collaborate with others, and undo mistakes.

**GitHub**: A cloud-based platform for hosting Git repositories, enabling collaboration, code sharing, and project management.

**GitHub Speckit**: GitHub's specification tool for creating structured project plans (dropped from author's stack in favor of OpenSpec).

**IDE (Integrated Development Environment)**: A software application that provides comprehensive tools for writing, testing, and debugging code all in one place.

**OpenSpec**: A specification framework tool that transforms plain language descriptions into comprehensive project plans, tasks, and technical documentation.

**Qwen CLI**: Alibaba's free, open-source coding assistant CLI that provides local or cloud-based AI assistance for development.

**Terminal**: A text-based interface for interacting with your computer's operating system by typing commands.

**TRAE**: A coding assistant tool with a prompt-based pricing model, offering good value but with limited context window.

**Traycer.ai**: An AI-powered development planning and validation tool (dropped from author's stack due to speed and cost issues).

**VS Code (Visual Studio Code)**: Microsoft's free, popular code editor with extensive plugin support and customization options.

**Warp**: A modern, GPU-accelerated terminal emulator with AI-powered command assistance and personalization options.

**Windsurf**: An AI-enhanced code editor with the Cascade agent and advanced context management features.

**Zed**: A fast, AI-first code editor built specifically for AI-assisted development with minimal resource usage and native AI integration.

---

## MCP (Model Context Protocol)

**Context7 MCP**: An MCP server that provides access to framework documentation and technical knowledge, helping AI assistants resolve issues by retrieving relevant documentation.

**DevTools MCP**: An MCP server for browser automation and testing, enabling AI agents to automatically navigate websites, collect errors, and debug frontend issues using Chrome DevTools.

**MCP (Model Context Protocol)**: A standard protocol that allows AI assistants to connect to external data sources and tools, extending their capabilities beyond their built-in knowledge.

**MCP Server**: A service that implements the Model Context Protocol, providing AI assistants with access to specific external resources like documentation, databases, or development tools.

**Sequential Thinking MCP**: An MCP server that forces AI assistants to think through problems systematically in structured steps before providing solutions, improving debugging quality and preventing impulsive decisions.

**Shadcn MCP**: An MCP server that enables AI assistants to browse, search, and install professional UI components from the shadcn/ui library.

**Task Manager MCP**: An MCP server that maintains task lists across different AI conversation sessions, ensuring development context is preserved and tasks require approval before completion.

---

## AI/ML & LLM Terms

**Agent**: An AI program that can perform tasks autonomously, such as writing code, debugging issues, or analyzing requirements with minimal human intervention.

**API Key**: A unique identifier that authenticates your access to an AI service or API, typically kept secret and stored securely.

**Caching**: Storing previously retrieved or generated data for reuse, reducing costs and improving response times in AI interactions.

**Fine-tuning**: The process of training an existing AI model on specific data to make it better at particular tasks.

**Frontier Model**: The most advanced, state-of-the-art AI models available, typically from major AI research companies like OpenAI, Anthropic, or Google.

**Hallucination**: When an AI model generates information that sounds plausible but is factually incorrect or made up.

**Inference**: The process of an AI model generating output (like code or text) based on your input prompt.

**LLM (Large Language Model)**: An AI system trained on vast amounts of text data that can understand and generate human-like text, used for tasks like coding assistance and conversation.

**Model Provider**: A company or service that offers access to AI models through APIs, such as OpenAI, Anthropic, or Google.

**Model Routing**: The intelligent selection of which AI model to use for different types of tasks to optimize for cost, speed, or quality.

**Open-Source Model**: An AI model whose code and weights are publicly available, allowing anyone to use, modify, or run it locally.

**Prompt**: The text input you provide to an AI model to request a specific response or action.

**Prompt Engineering**: The practice of crafting effective prompts to get better results from AI models.

**Rate Limiting**: Restrictions on how many requests you can make to an AI service within a specific time period.

**Token**: The basic unit of text that AI models process, roughly equivalent to a word or part of a word. AI pricing and limits are typically measured in tokens.

---

## AI Model Providers

**Factory AI**: An AI platform offering competitive token pricing with advanced caching, providing access to models like GPT-5-high and codex at reduced costs through the Droid CLI tool.

**GLM (GLM Coding Plan)**: A cost-effective AI model provider offering state-of-the-art open-source models with generous usage limits, serving as the author's main LLM for development work.

**Synthetic.new**: A privacy-first AI model provider offering access to 20+ frontier open-source models with competitive pricing and high rate limits, emphasizing code privacy and fast performance.

---

## Web Development & Technologies

**Astro**: A modern web framework focused on generating static HTML with minimal JavaScript, optimized for fast-loading websites and excellent performance scores.

**bcrypt**: A password hashing algorithm used to securely store user passwords by converting them into irreversible encrypted strings.

**CDN (Content Delivery Network)**: A network of servers distributed globally that deliver web content to users from the closest server, improving loading speed.

**Cloudflare Functions**: Serverless backend functions that run on Cloudflare's edge network, allowing you to add dynamic features to static sites.

**Cloudflare Pages**: A free static website hosting platform with global CDN, automatic deployments from Git, and built-in support for serverless functions.

**Cloudflare Workers**: Serverless compute platform that runs JavaScript code on Cloudflare's global network, offering 100,000 free requests per day.

**CORS (Cross-Origin Resource Sharing)**: A security mechanism that controls which websites can access your API or resources from a different domain.

**D1 Database**: Cloudflare's serverless SQL database service, designed to work seamlessly with Cloudflare Workers and Pages.

**Edge Functions**: Small pieces of code that run on CDN edge servers close to users, providing fast response times for dynamic content.

**Island Architecture**: A web development pattern where most of a page is static HTML with small "islands" of interactive JavaScript components, improving performance.

**Jamstack**: A web development architecture emphasizing JavaScript, APIs, and Markup (static files), resulting in fast, secure, and scalable websites.

**JWT (JSON Web Token)**: A secure way to transmit information between parties as a JSON object, commonly used for user authentication in web applications.

**Middleware**: Software that sits between different application components, often used for authentication, logging, or request processing before reaching the main application.

**Next.js**: A popular React framework that supports server-side rendering, static site generation, and API routes for building full-stack web applications.

**React**: A JavaScript library for building user interfaces using reusable components, maintained by Meta (Facebook).

**SSG (Static Site Generation)**: The process of building all web pages as static HTML files at build time rather than when users request them, resulting in faster loading.

**SSR (Server-Side Rendering)**: Generating HTML for web pages on the server for each request, allowing for dynamic content while improving SEO and initial load time.

**Svelte**: A modern JavaScript framework that compiles components into highly efficient vanilla JavaScript at build time, resulting in smaller bundle sizes.

**Tailwind CSS**: A utility-first CSS framework that provides small, composable classes for styling HTML directly, enabling rapid UI development without writing custom CSS.

**Turnstile**: Cloudflare's privacy-focused alternative to CAPTCHA for protecting websites from spam and bots.

**WebSocket**: A communication protocol that provides full-duplex (two-way) communication between a web browser and server, enabling real-time features.

---

## Software Development Practices

**Acceptance Criteria**: Specific conditions that must be met for a feature or task to be considered complete and acceptable.

**ADR (Architecture Decision Record)**: A document that captures an important architectural decision, its context, and consequences for future reference.

**API (Application Programming Interface)**: A set of rules and protocols that allows different software applications to communicate with each other.

**Branch**: In Git, a separate line of development that allows you to work on features without affecting the main codebase.

**CI/CD (Continuous Integration/Continuous Deployment)**: Automated processes that test code changes and deploy them to production, reducing manual work and errors.

**Code Review**: The practice of having other developers examine your code for quality, bugs, and adherence to standards before merging it.

**Commit**: In Git, saving a snapshot of your code changes with a descriptive message about what was changed.

**Debugging**: The process of finding and fixing errors or unexpected behavior in code.

**Deployment**: The process of releasing your code to a server or platform where users can access it.

**Edge Case**: An unusual or rare situation that might cause errors if not properly handled in code.

**Feature Branch**: A Git branch created specifically for developing a single feature, keeping it isolated from the main codebase until complete.

**Main Branch**: The primary Git branch (often called "main" or "master") that contains the production-ready code.

**Merge Request / Pull Request**: A request to merge code changes from one Git branch into another, typically including code review before approval.

**Migration**: A script or process that updates a database structure (schema) or moves data from one system to another.

**MVP (Minimum Viable Product)**: The simplest version of a product that has just enough features to be usable and provide value to early users.

**PRD (Product Requirements Document)**: A document that describes what a product should do, who will use it, and what problems it solves.

**Push**: In Git, uploading your local code changes to a remote repository (like GitHub).

**Refactoring**: Restructuring existing code to improve its quality, readability, or performance without changing what it does.

**Regression**: When a code change accidentally breaks existing functionality that was previously working.

**Remote Repository**: A version of your Git repository stored on a server (like GitHub), allowing backup and collaboration.

**REST API**: A standard way to create web APIs using HTTP methods (GET, POST, PUT, DELETE) to interact with server resources.

**Rollback**: Reverting code to a previous version, typically done when a deployment causes problems in production.

**SaaS (Software as a Service)**: Software delivered over the internet as a service, typically through a subscription model.

**Schema**: The structure and organization of a database, defining tables, columns, and relationships.

**Serverless**: A cloud computing model where you write functions that run on-demand without managing servers, paying only for execution time.

**Staging Environment**: A testing environment that closely mirrors production, used to validate changes before releasing to users.

**Technical Debt**: The implied cost of future rework caused by choosing quick, easy solutions now instead of better approaches that take longer.

**Unit Test**: A test that verifies a single, small piece of code (like a function) works correctly in isolation.

**User Story**: A description of a feature from an end-user's perspective, typically following the format "As a [user], I want [goal] so that [reason]".

**Version Control**: A system (like Git) that tracks changes to files over time, allowing you to review history and revert to previous versions.

---

## Core Web Vitals & Performance

**Bundle Size**: The total file size of JavaScript and CSS that browsers must download to run a web application, affecting loading speed.

**CLS (Cumulative Layout Shift)**: A Core Web Vitals metric measuring visual stability - how much page content unexpectedly shifts during loading.

**Core Web Vitals (CWV)**: Google's set of metrics measuring website performance and user experience, including loading speed, interactivity, and visual stability.

**FCP (First Contentful Paint)**: A performance metric measuring how long it takes for the first piece of content to appear on screen.

**Hydration**: The process of making a static HTML page interactive by attaching JavaScript event handlers and state.

**Lazy Loading**: Delaying the loading of images or content until they're needed (e.g., when scrolling into view), improving initial page load time.

**LCP (Largest Contentful Paint)**: A Core Web Vitals metric measuring how long it takes for the largest visible content element to load.

**PageSpeed**: Google's tool and metrics for measuring website performance and providing optimization recommendations.

**Partial Hydration**: Loading JavaScript only for interactive components rather than the entire page, reducing initial bundle size.

**TTFB (Time To First Byte)**: A performance metric measuring how long it takes for a browser to receive the first byte of data from a server.

---

## File Formats & Configuration

**Environment Variables**: Configuration values (like API keys) stored separately from code, typically in .env files, for security and flexibility.

**JSON (JavaScript Object Notation)**: A text format for storing and exchanging data using human-readable key-value pairs and arrays.

**Markdown (.md)**: A lightweight text format using simple symbols for formatting (like # for headings, * for lists), easily readable as plain text.

**YAML (YAML Ain't Markup Language)**: A human-readable data format commonly used for configuration files, using indentation to show structure.

---

## Development Workflow & Tools

**Branch Strategy**: A plan for organizing Git branches in a project, such as using feature branches for development and main branch for production.

**Build Process**: The steps that convert source code into a deployable application, including compiling, bundling, and optimizing.

**Build Time**: The phase when your code is compiled and prepared for deployment, as opposed to runtime when users interact with it.

**Deployment Script**: Automated commands that handle the process of releasing code to production servers.

**Hot Reload**: A development feature that automatically updates your application in the browser when you change code, without losing state.

**Local Development**: Running and testing your application on your own computer before deploying it to a server.

**Package Manager**: A tool (like npm, yarn, or pnpm) that installs and manages code libraries and dependencies for your project.

**Plugin**: Additional software that extends the functionality of a primary application, like VS Code extensions.

**Production Environment**: The live server/system where your application runs for real users.

**Sandbox**: An isolated environment for safely testing code without affecting production systems.

**Task Breakdown**: Dividing a large feature into smaller, manageable tasks that can be implemented and tested individually.

**Workflow**: A sequence of steps or processes followed to accomplish development tasks efficiently.

---

## Security & Authentication

**API Endpoint**: A specific URL in an API that performs a particular function, like /api/login for user authentication.

**Authentication**: The process of verifying a user's identity, typically through username and password.

**Authorization**: Determining what actions or resources an authenticated user is allowed to access.

**CSRF (Cross-Site Request Forgery)**: A security vulnerability where attackers trick users into performing unwanted actions on websites where they're authenticated.

**Hash**: A one-way cryptographic function that converts data (like passwords) into a fixed-length string that cannot be reversed.

**Input Validation**: Checking user input to ensure it meets expected formats and doesn't contain malicious code before processing.

**OAuth**: An authorization standard allowing users to grant applications access to their information without sharing passwords.

**Password Hashing**: Converting plain-text passwords into irreversible encrypted strings before storing them in a database.

**Rate Limiting**: Restricting how many requests a user can make to an API within a time period, preventing abuse.

**Sanitization**: Cleaning user input by removing or escaping potentially dangerous characters before using it.

**Session**: A period of interaction between a user and an application, typically maintained through cookies or tokens.

**SQL Injection**: A security vulnerability where attackers insert malicious SQL code through user input to manipulate databases.

**XSS (Cross-Site Scripting)**: A security vulnerability where attackers inject malicious scripts into websites viewed by other users.

---

## Development Concepts

**Abstraction**: Hiding complex implementation details behind simpler interfaces, making code easier to use and understand.

**Async/Await**: A JavaScript syntax for handling asynchronous operations in a more readable, sequential style.

**Boilerplate**: Standard, repetitive code that's needed in many places but doesn't vary much between implementations.

**Breaking Change**: A code change that causes existing functionality to stop working, requiring updates to dependent code.

**Codebase**: The complete collection of source code for a project.

**Component**: A reusable, self-contained piece of code (like a button or form) that can be used in multiple places.

**Dependency**: External code libraries or packages that your project relies on to function.

**Design Pattern**: A reusable solution to common programming problems, providing proven approaches to structure code.

**DRY (Don't Repeat Yourself)**: A coding principle emphasizing code reuse to avoid duplication and maintenance issues.

**Endpoint**: See **API Endpoint**.

**Fallback**: An alternative option used when the primary approach fails or isn't available.

**Framework**: A structured foundation of code that provides common functionality, allowing you to build applications faster by following its patterns.

**Library**: A collection of pre-written code that provides specific functionality you can use in your projects.

**Localhost**: The address (usually http://localhost or 127.0.0.1) used to access your application running on your own computer.

**Monorepo**: A single repository containing multiple related projects or packages, managed together.

**Namespace**: A container that organizes code elements (like variables or functions) to avoid naming conflicts.

**npm (Node Package Manager)**: The default package manager for JavaScript, used to install and manage code libraries.

**Payload**: The actual data sent in an API request or response, excluding headers and metadata.

**Polyfill**: Code that provides modern functionality in older browsers that don't support it natively.

**Query**: A request for data from a database or API.

**Repository (Repo)**: A storage location for code, typically managed with Git, containing all project files and their history.

**Scope**: The portion of code where a variable or function is accessible and can be used.

**SDK (Software Development Kit)**: A collection of tools, libraries, and documentation for developing applications on a specific platform.

**Single Responsibility Principle**: A design principle stating that each module or function should have only one reason to change.

**Stack**: The combination of technologies used in a project, such as "Astro + Tailwind + Cloudflare Pages".

**Stack Trace**: A report showing the sequence of function calls that led to an error, useful for debugging.

**Syntax**: The rules and structure for writing valid code in a programming language.

**Type**: A classification of data (like string, number, or boolean) that determines what operations can be performed on it.

**TypeScript**: A programming language that extends JavaScript by adding optional type checking for better error detection.

---

## Acronyms Quick Reference

- **ADR**: Architecture Decision Record
- **API**: Application Programming Interface
- **BYOK**: Bring Your Own Key
- **CDN**: Content Delivery Network
- **CI/CD**: Continuous Integration/Continuous Deployment
- **CLI**: Command-Line Interface
- **CLS**: Cumulative Layout Shift
- **CORS**: Cross-Origin Resource Sharing
- **CSRF**: Cross-Site Request Forgery
- **CWV**: Core Web Vitals
- **DRY**: Don't Repeat Yourself
- **FCP**: First Contentful Paint
- **IDE**: Integrated Development Environment
- **JSON**: JavaScript Object Notation
- **JWT**: JSON Web Token
- **LCP**: Largest Contentful Paint
- **LLM**: Large Language Model
- **MCP**: Model Context Protocol
- **MVP**: Minimum Viable Product
- **npm**: Node Package Manager
- **OAuth**: Open Authorization
- **PRD**: Product Requirements Document
- **REST**: Representational State Transfer
- **ROI**: Return On Investment
- **SaaS**: Software as a Service
- **SDK**: Software Development Kit
- **SEO**: Search Engine Optimization
- **SQL**: Structured Query Language
- **SSG**: Static Site Generation
- **SSR**: Server-Side Rendering
- **TTFB**: Time To First Byte
- **UI**: User Interface
- **URL**: Uniform Resource Locator
- **UX**: User Experience
- **XSS**: Cross-Site Scripting
- **YAML**: YAML Ain't Markup Language

---

Back to index: [Top‑level README](../README.md)
