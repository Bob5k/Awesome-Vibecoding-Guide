# Tool Compatibility ⚙️

## Core Integration Requirements

This guide describes in general how tools should be compatible with the Awesome Vibecoding Guide approach. The recommended subset of tools (Zed, Droid CLI / Claude Code) are designed to provide optimal performance and are author's choices, however other tools can be used as well. For optimal compatibility, tools should support:

### 1. Bring Your Own Key (BYOK) Integration
- **External LLM API Support**: Essential for cost efficiency and model flexibility
- **Custom Endpoint Configuration**: Ability to connect to your preferred LLM providers
- **API Key Management**: Secure handling of multiple API keys and providers

### 2. MCP (Model Context Protocol) Server Support
- **External Source Integration**: Connect to documentation, databases, and external resources
- **Development Efficiency**: Streamlined access to relevant context and tools
- **Robustness**: Enhanced reliability through multiple data sources

## Compatible Tools

### CLI-Based Coding Agents
- **Droid CLI**: Command-line interface with BYOK support
- **Claude Code**: Anthropic's CLI tool with API integration
- **AmpCode**: Alternative CLI coding assistant
- **Codex**: GitHub's coding assistant tool
- **Other similar CLI agents**: Any tool supporting external LLM APIs

### IDEs and Editors with Plugin Support
- **Zed**: Fast, modern code editor with extensibility
- **VS Code**: Wide plugin ecosystem and MCP support
- **Cursor**: AI-powered IDE with external model support
- **Cursor AI**: Advanced AI integration capabilities

### AI Assistant Plugins
- **Kilo**: AI coding assistant plugin
- **Roo**: Development assistant with external integration
- **Cline**: Enhanced AI assistant for development
- **Continue**: Open-source AI assistant with BYOK support

## Integration Benefits

### Cost Efficiency
- **GLM Integration**: Use cost-effective models where appropriate
- **Provider Flexibility**: Switch between providers based on task complexity
- **Usage Optimization**: Route requests to the most cost-effective models

### Development Efficiency
- **Context Awareness**: MCP servers provide relevant project context
- **Tool Orchestration**: Seamless integration between development tools
- **Real-time Assistance**: Immediate access to relevant documentation and resources

### Robustness and Reliability
- **Multiple Data Sources**: Reduced dependency on single providers
- **Fallback Mechanisms**: Backup options for model and data access
- **Extensibility**: Easy addition of new tools and integrations

## Not Recommended Combinations

- **Closed Platforms**: Replit, Lovable, Bolt (limited integration options)
- **MCP Server Overload**: Too many MCP servers simultaneously (performance impact)
- **Locked-in Tools**: Platforms without BYOK or external API support
- **Single-vendor Dependencies**: Tools that lock you into one ecosystem

## Implementation Guidelines

1. **Start with Core Tools**: Begin with Droid CLI or Claude Code
2. **Gradual Integration**: Add MCP servers as needed
3. **API Management**: Set up secure API key handling
4. **Monitor Usage**: Track costs and performance across providers
5. **Flexibility First**: Choose tools that support multiple integration methods

Back: [Tools & Tech Stack](./README.md)
