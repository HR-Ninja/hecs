# HECS: Minimal C Entity-Component System

HECS is a small, efficient, and standalone Entity-Component System (ECS) implemented in C. It's designed for high-performance game loops and simulations with thousands of entities and components.

## Features

- ✅ Dead entity reuse (freelist)
- ✅ Lazy, on-demand component memory allocation
- ✅ Fast SoA layout for cache efficiency
- ✅ Bitmask-based component querying
- ✅ Fits in a single header file

## Usage

### 1. Create Entities

```c
Entity e = create_entity();
```

### 2. Register Components

```c
typedef struct {
    float x, y;
} Position;

Component PositionComponent = register_component(sizeof(Position));
```

### 3. Attach Components

```c
Position p = {1.0f, 2.0f};
attach_component(e, PositionComponent, &p);
```

### 4. Access Components

```c
Position* p = (Position*)get_component(e, PositionComponent);
```

### 5. Remove Components

```c
remove_component(e, PositionComponent);
```

### 6. Destroy Entities

```c
destroy_entity(e);
```

## Constants

- `MAX_ENTITIES` — Maximum number of entities (default: 20,000)
- `MAX_COMPONENTS` — Maximum number of component types (default: 64)

## Bitmask Query

Use `HAS_COMPONENT(mask, id)` macro to check if an entity has a specific component.

```c
if (HAS_COMPONENT(entity_mask[e], PositionComponent)) { ... }
```

## Cleanup

Call this to free all allocated component memory:

```c
free_components();
```

## License

Public domain / MIT — do whatever you want.

---

Made for fun, games, and systems programming.
