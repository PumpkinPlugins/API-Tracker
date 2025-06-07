# Core Infrastructure

Essential building blocks and foundational systems that other APIs depend on.

## Packet Wrappers

**Status**: 🔴 Not Started
**Priority**: High
**Dependencies**: None

Abstraction layer over raw Minecraft protocol packets to provide a safer, more ergonomic API for plugin developers.

### Requirements
- Type-safe packet construction and decoding
- Automatic version compatibility handling
- Performance-optimized packet serialization
- Plugin-friendly error handling

---

## NamespacedKeys

**Status**: 🔴 Not Started
**Priority**: High
**Dependencies**: None

A system for uniquely identifying resources, items, and other game objects using namespace:key format.

### Requirements
- Standard namespace:key format support
- Plugin namespace management
- Conflict resolution for duplicate keys
- Integration with resource loading systems

---

## PersistentDataContainers

**Status**: 🔴 Not Started
**Priority**: High
**Dependencies**: NamespacedKeys, NBT API

A system for storing custom data on entities, items, blocks, and other game objects that survives server restarts.

### Requirements
- Type-safe data storage and retrieval
- Automatic serialization/deserialization
- Integration with game saving systems
- Performance optimization for frequent access

---

## AdventureLib Integration

**Status**: 🔴 Not Started
**Priority**: Medium
**Dependencies**: Packet Wrappers

Integration or Rust rewrite of Adventure library features for rich text, components, and formatting.

### Requirements
- Text component system
- Color and formatting support
- Click and hover events
- Serialization to/from various formats (JSON, MiniMessage, etc.)

---

## Plugin Dependency System

**Status**: 🔴 Not Started
**Priority**: High
**Dependencies**: None

System for managing plugin dependencies and load order through TOML configuration.

### Requirements
- Dependency declaration in plugin TOML
- Automatic dependency resolution
- Version compatibility checking
- Graceful handling of missing dependencies

---

## Event Registry

**Status**: 🔴 Not Started
**Priority**: High
**Dependencies**: None

System for registering and handling both built-in and custom events.

### Requirements
- Custom event creation and registration
- Event priority system
- Asynchronous event handling
- Performance monitoring and debugging tools

---

## Task Scheduler

**Status**: 🔴 Not Started
**Priority**: High
**Dependencies**: None

Bukkit-style scheduler for running tasks asynchronously, delayed, or at intervals.

### Requirements
- Delayed task execution
- Repeating tasks with configurable intervals
- Async task support
- Task cancellation and management
- Thread-safe execution

---

## Database Support

**Status**: 🔴 Not Started
**Priority**: Medium
**Dependencies**: None

Basic database connectivity and ORM support using SQLx.

### Requirements
- SQLite, MySQL, and PostgreSQL support
- Connection pooling
- Migration system
- Async database operations
- Plugin-specific database isolation
