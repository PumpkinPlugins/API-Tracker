# API Design Principles

This document outlines the core principles that guide the design and implementation of the Pumpkin Plugin API.

## 🎯 Core Philosophy

The Pumpkin Plugin API is designed to be **powerful, safe, and ergonomic**. We prioritize developer experience while maintaining the performance and safety that Rust provides.

## 🏗️ Design Principles

### 1. Rust-First Design

**Principle**: Embrace Rust's strengths rather than simply porting Java APIs.

- **Ownership**: Use Rust's ownership system to prevent common plugin errors
- **Type Safety**: Leverage the type system to catch errors at compile time
- **Memory Safety**: Eliminate entire classes of runtime errors through safe APIs
- **Zero-Cost Abstractions**: Provide high-level APIs that compile to efficient code

**Example**:
```rust
// Instead of nullable returns like Java Bukkit
player.get_item_in_hand() // Returns Option<ItemStack>

// Use Result for operations that can fail
world.set_block(pos, block_type).await? // Returns Result<(), WorldError>
```

### 2. Async-First Architecture

**Principle**: Design APIs to be non-blocking by default.

- **Main Thread Protection**: Prevent plugins from blocking the server tick
- **Concurrent Operations**: Enable plugins to perform multiple operations simultaneously
- **Async/Await**: Use Rust's async/await syntax for intuitive asynchronous code
- **Backpressure**: Handle resource limits gracefully

**Example**:
```rust
// Async teleportation that doesn't block the server
player.teleport_async(location).await?;

// Concurrent operations
let (health, hunger) = tokio::join!(
    player.get_health(),
    player.get_hunger()
);
```

### 3. Builder Pattern for Complex Objects

**Principle**: Use builders for creating complex objects with many optional parameters.

- **Fluent Interface**: Chain method calls for readable object construction
- **Type Safety**: Use the type system to enforce required parameters
- **Defaults**: Provide sensible defaults for optional parameters
- **Validation**: Validate parameters at build time when possible

**Example**:
```rust
let item = ItemStack::builder()
    .item_type(Material::Diamond_Sword)
    .name("Legendary Blade")
    .lore(vec!["A sword of great power"])
    .enchantment(Enchantment::Sharpness, 5)
    .unbreakable(true)
    .build()?;
```

### 4. Event-Driven Architecture

**Principle**: Use events for loose coupling and extensibility.

- **Observer Pattern**: Allow multiple plugins to react to the same events
- **Priority System**: Control event handler execution order
- **Cancellation**: Allow events to be cancelled by handlers
- **Custom Events**: Enable plugins to create and fire their own events

**Example**:
```rust
#[event_handler(priority = EventPriority::High)]
async fn on_player_join(event: &mut PlayerJoinEvent) {
    if should_cancel_join(&event.player).await {
        event.cancel();
    }
}
```

### 5. Resource Management

**Principle**: Automatic resource cleanup with explicit control when needed.

- **RAII**: Use Rust's ownership system for automatic cleanup
- **Explicit Lifetimes**: Make resource lifetimes clear and controlled
- **Graceful Shutdown**: Ensure resources are properly cleaned up on server stop
- **Leak Prevention**: Prevent memory and handle leaks in long-running servers

**Example**:
```rust
// Task is automatically cancelled when dropped
let _task = scheduler.run_later(Duration::from_secs(10), || {
    // This cleanup happens automatically
}).await?;

// Or explicit control
let task = scheduler.run_repeating(interval, callback).await?;
// ... later
task.cancel().await;
```

### 6. Configuration and Serialization

**Principle**: Use Rust's serialization ecosystem for configuration.

- **Serde Integration**: Use serde for serializing/deserializing data
- **Multiple Formats**: Support TOML, JSON, and YAML configuration
- **Type Safety**: Leverage Rust's type system for configuration validation
- **Migration**: Provide tools for configuration migration

**Example**:
```rust
#[derive(Serialize, Deserialize)]
struct PluginConfig {
    enabled_features: Vec<String>,
    max_players_per_team: u32,
    #[serde(default = "default_timeout")]
    timeout_seconds: u64,
}
```

### 7. Performance Considerations

**Principle**: Design APIs that encourage performant usage patterns.

- **Batch Operations**: Provide batch APIs for operations on multiple objects
- **Lazy Evaluation**: Use iterators and lazy evaluation where appropriate
- **Memory Pools**: Reuse objects to reduce allocation pressure
- **Profiling Integration**: Built-in profiling and performance monitoring

**Example**:
```rust
// Batch operation instead of individual calls
world.set_blocks(block_changes).await?;

// Lazy iteration over large datasets
for player in server.players().filter(|p| p.is_online()) {
    // Process each player
}
```

### 8. Error Handling Strategy

**Principle**: Provide clear, actionable error information.

- **Specific Error Types**: Use different error types for different failure modes
- **Error Context**: Include context about what operation failed and why
- **Recovery**: Provide information about how to recover from errors
- **Logging Integration**: Automatic error logging with appropriate levels

**Example**:
```rust
#[derive(Error, Debug)]
enum PlayerError {
    #[error("Player {name} not found")]
    NotFound { name: String },

    #[error("Player {name} is offline")]
    Offline { name: String },

    #[error("Insufficient permissions: {required}")]
    InsufficientPermissions { required: String },
}
```

### 9. Backwards Compatibility

**Principle**: Minimize breaking changes and provide migration paths.

- **Semantic Versioning**: Follow semver for API versioning
- **Deprecation Warnings**: Provide advance warning before removing APIs
- **Migration Guides**: Document how to migrate between API versions
- **Compatibility Layers**: Provide temporary compatibility when possible

### 10. Documentation and Examples

**Principle**: APIs should be self-documenting with comprehensive examples.

- **Doc Comments**: Every public API should have documentation
- **Examples**: Include code examples in documentation
- **Tutorials**: Provide step-by-step guides for common tasks
- **Best Practices**: Document recommended usage patterns

## 🔄 API Evolution

### Adding New Features
1. Design with future extensibility in mind
2. Consider how the feature fits into the existing ecosystem
3. Provide both simple and advanced usage patterns
4. Include comprehensive tests and documentation

### Modifying Existing APIs
1. Prefer additive changes over breaking changes
2. Use deprecation warnings for removed functionality
3. Provide migration tools and documentation
4. Consider the impact on existing plugins

### Removing Features
1. Deprecate features before removing them
2. Provide alternative solutions
3. Give developers time to migrate
4. Document the removal in changelog and migration guide

## 🧪 Testing Strategy

### API Testing
- Unit tests for individual components
- Integration tests for feature interactions
- Performance tests for critical paths
- Compatibility tests with Minecraft versions

### Plugin Testing
- Provide testing utilities for plugin developers
- Mock implementations for testing without a full server
- Test harnesses for event handling
- Performance profiling tools

This document serves as a living guide for API development and should be updated as the project evolves.
