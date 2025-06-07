# Contributing to Pumpkin Plugin API

Thank you for your interest in contributing to the Pumpkin Plugin API! This document provides guidelines and information for contributors.

## 🚀 Getting Started

### Prerequisites
- Rust (latest stable version)
- Familiarity with Minecraft server mechanics
- Understanding of plugin API design principles
- Knowledge of async Rust programming

### Development Setup
1. Fork the repository
2. Clone your fork locally
3. Set up the development environment
4. Run tests to ensure everything works

## 📋 How to Contribute

### Choosing What to Work On
1. Browse the [main README](./README.md) for available features
2. Check the [GitHub Issues](https://github.com/PumpkinPlugins/API-Tracker/issues) for specific tasks
3. Look for issues labeled `good first issue` if you're new
4. Comment on an issue to claim it before starting work

### Implementation Process
1. **Research**: Understand the feature requirements thoroughly
2. **Design**: Consider API ergonomics and Rust best practices
3. **Implement**: Write the code following our guidelines
4. **Test**: Add comprehensive tests for your implementation
5. **Document**: Update documentation and add examples
6. **Submit**: Create a pull request with clear description

## 🎯 Implementation Priorities

### High Priority
Features that other systems depend on should be implemented first:
- Core Infrastructure components
- Basic player and world management
- Essential item and inventory systems

### Medium Priority
Features that enhance gameplay but aren't blocking other development:
- Advanced player management features
- Visual effects and particle systems
- Teams and scoreboard APIs
- Custom crafting recipes

### Low Priority
Nice-to-have features that can be implemented later:
- Custom enchantments
- NPC API
- Advanced PvP management
- Complex visual effects

## 🏗️ Architecture Guidelines

### API Design Principles
- **Ergonomic**: APIs should be intuitive and easy to use
- **Type Safe**: Leverage Rust's type system to prevent errors
- **Async First**: Use async/await for operations that might block
- **Memory Safe**: No unsafe code without exceptional justification
- **Performance**: Consider performance implications of all APIs

### Code Structure
```
pumpkin/src/plugin/
├── api/            # Core infrastructure
├── loader/         # Player management APIs
└── mod.rs          # Main library exports
```

### Error Handling
- Use `Result<T, E>` for fallible operations
- Define specific error types for different API categories
- Provide helpful error messages for plugin developers
- Consider recovery strategies where appropriate

### Async Patterns
- Use `tokio` for async runtime
- Prefer async APIs for I/O operations
- Use channels for cross-thread communication
- Document thread safety guarantees

## 📝 Code Standards

### Rust Style
- Follow official Rust style guidelines
- Use `rustfmt` for consistent formatting
- Run `clippy` and address all warnings
- Write comprehensive documentation comments

### Documentation
- Document all public APIs with examples
- Include usage patterns and common pitfalls
- Update relevant documentation files
- Add examples to the `examples/` directory

### Testing
- Write unit tests for all functionality
- Include integration tests for complex features
- Test error conditions and edge cases
- Ensure tests are deterministic and reliable

## 🔍 Review Process

### Pull Request Guidelines
1. **Clear Title**: Describe what the PR accomplishes
2. **Detailed Description**: Explain the changes and reasoning
3. **Issue References**: Link to related issues
4. **Testing**: Describe how the changes were tested
5. **Breaking Changes**: Clearly mark any breaking changes

### Review Criteria
- Code quality and adherence to guidelines
- API design and ergonomics
- Performance implications
- Documentation completeness
- Test coverage and quality

## 📚 Resources

### Helpful Links
- [The Pumpkin project](https://github.ccom/Pumpkin-MC/Pumpkin)
- [Rust Book](https://doc.rust-lang.org/book/)
- [Async Book](https://rust-lang.github.io/async-book/)
- [Minecraft Protocol Documentation](https://minecraft.wiki/w/Minecraft_Wiki:Projects/wiki.vg_merge)
- [Bukkit API Reference](https://hub.spigotmc.org/javadocs/bukkit/)
- [Paper API Reference](https://papermc.io/javadocs/)

### Communication
- Join our [Discord](https://discord.gg/JMwGrM6c) server for real-time discussion
- Use GitHub Issues for feature requests and bug reports
- Tag maintainers for urgent issues or questions

## 🏷️ Issue Labels

- `enhancement`: New feature or improvement
- `bug`: Something isn't working correctly
- `documentation`: Documentation needs attention
- `good first issue`: Good for newcomers
- `help wanted`: Community help needed
- `priority-high`: Should be addressed soon
- `breaking-change`: Will break existing APIs

## 🎉 Recognition

Contributors are recognized in several ways:
- Listed in the repository contributors
- Mentioned in release notes for significant contributions
- Invited to join the contributor team for ongoing contributors
- Special recognition for major feature implementations

## ❓ Questions?

If you have questions about contributing:
1. Check existing documentation and issues
2. Ask in our Discord community
3. Create a GitHub issue with the `question` label
4. Reach out to maintainers directly for urgent matters

Thank you for helping make Pumpkin's plugin API amazing! Every contribution, no matter how small, helps the entire Minecraft server community.
