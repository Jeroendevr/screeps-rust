# Task list

```
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
## Question
How to type a list of enums with a unkown size at compile time?

## Roles

Add role Harvester to currently spawning creeps

### Provide the role to the Creep using

SpawnOptions::new().memory()
Where memory needs a jsValue if the form of { role: harvester } which is an object
