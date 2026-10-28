# Powder
 
Powder is a compiled programming language that combines the memory safety and performance of Rust with a syntax designed to be as readable as Python. It is intended for scientific simulation and data-intensive work, where native speed matters but low-level memory management should not stand in the way.
 
Powder is in the early design stage. A compiler does not exist yet, and this repository currently contains the language specification.
 
## Example
 
```
struct Particle:
    var position: Float = 0.0
    var velocity: Float = 1.0
 
    mut fn step(dt: Float):
        position += velocity * dt
 
fn main():
    var p = Particle()
    for i in 0..100:
        p.step(0.01)
    print(p.position)
```
 
```
powder run sample.powder
```
 
## Design principles
 
1. Value semantics. Every variable owns its data, and copies of large values are always explicit.
2. Visible mutation. Functions that modify data are marked with mut, at both the definition and the call site.
3. No lifetimes. References cannot be stored or returned. Persistent links use versioned handles, and the compiler requires every lookup to account for the possibility that the target no longer exists.
4. No null values. Optional types are written as T? and must be checked before use.
5. Clear diagnostics. Every error message states what went wrong, where it occurred, and how to resolve it.
## Implementation
 
The Powder compiler is written in Rust. It validates a program against the rules above, translates it into Rust source code, and passes the result to rustc to produce a native executable. Any failure in the generated Rust is treated as a compiler defect rather than a user error.
 
## Roadmap
 
1. Language specification
2. Lexer
3. Parser
4. Type and ownership checking
5. Rust code generation
6. Command line tooling: powder run, powder build, and powder new
## License
 
Powder is released under the MIT License.
