# Task list

## 2025 Notes and questions

### Build Tower

- [ ] Make a builder role
  - [ ] Make one builder regardless of other creep
    - [ ] Count creep per role
      - [ ] What is the best way to count the creep, call the creep memory, this needs a Rust-JS call or can it be done
        withing Rust?

#### Role Harvester

- [x] Harvester Creep only have 'harvester' stored not the dict 'role:harvester' try that first

## Keep rust on 1.81

### Upgrade to 0.23.0 of the screeps-game-api

Error message for return

```rust
fn spawn_creep(spawn: &StructureSpawn, body: &[Part; 4], name: &str) -> Result<(), screeps::ErrorCode> {
    info!("spawn spawning is {}, with body {:?} and given name {}",spawn.name(), body, name);
    match spawn.spawn_creep(body, name) {
        Ok(()) => Ok(()),
        Err(e) => {
            warn!("couldn't spawn: {:?}", e);
            Err(e)
        }
}
```

Error types do not have to be imported with their hierarchy to be used

```rust
fn spawn_creep(spawn: &StructureSpawn, body: &[Part; 4], name: &str) -> Result<(), SpawnCreepErrorCode>;
```

```rust
// Import is
use screeps::action_error_codes::*,

screeps::enums::action_error_codes::structurespawn_error_code

```

The following block to spawn_creeps has been modified

```rust
fn spawn_creep(spawn: &StructureSpawn, &body: &[Part;4], name: &str) -> Result<(), Self::Error>{
    
match spawn.spawn_creep(&body, &name) {
    Ok(()) => additional += 1,
    Err(e) => warn!("couldn't spawn: {:?}", e),
    }
}
```

Question, how to handle this so that an OK is sufficient?
TODO make a small example how error handling is done.

### Visualize path of screeps

`move_to` has a optional param called `visualizePathStyle`. Implement that one

## 2024 Notes and questions

```rust
match spawn.spawn_creep(&body, &name) {
                Ok(()) => additional += 1,
                Err(e) => warn!("couldn't spawn: {:?}", e),
}
```

Implement as a function

```rust
fn spawn_creep(spawn: &StructureSpawn) {
    info!("spawn spawning is {}",spawn.name())
}
```

### Question
How to type a list of enums with a unkown size at compile time?

### Roles

Add role Harvester to currently spawning creeps

### Provide the role to the Creep using

SpawnOptions::new().memory()
Where memory needs a jsValue if the form of { role: harvester } which is an object
Add a memory object of enums to the memory

> Learn about the wasm-bindgen crate on rust
> Learn how to create a Javascript object from rust so it satisfies JsValue

Follow tutorial on https://rustwasm.github.io/docs/book/

Game of Life example does not work anymore.
The src code of wasm-pack-template https://github.com/rustwasm/wasm-pack-template/blob/master/src/lib.rs
lists other source code than the book but I cannot manage this source code to work.

Updating cargo to 2021 edition and upgrading all npm packages did not made an improvement.
[x] Look through wasm-bindgen docs to see what is correct use of display alert
The simple mozilla tutorial resulted in the same error. So it has probably to do with webassemblyjs

### wasm-bindgen dependency.

Mogelijk testen met diverse wasm-bindgen versies omdat de wasm binary mogelijk onleesbaar is door de parser

From wasm-bindgen =0.2.93" gecompileerde binaries worden niet goed door webpack geparsed

#### Following steps leads to workable

wasm-pack 0.2.93

- wasm-pack build --target bundler
- cd site
- npm run build
- npm run serve

### Non workable

wasm-pack 0.2.95

- wasm-pack build --target bundler

Solution is to keep on rust 1.81

#### Representation Attributes (Attribute like macro's)

Omdat de representatie van Rust naar JS belangrijk is om argumenten en return waarde vast te leggen zijn er 'attribute
like macros'
zoals `#[repr(u8)]`. Macro's worden behandeld in de rustlings course hfd 21.

##### Rustlings course volgen tm hfd 21



