Speck Driven Development is a methodology where a formal detailed specification serves as a blueprint for AI code generation.

*SDD provides a deterministic control plane turning architecture into a runtime invariant that is actively maintained by the system itself.*

In SDD the **spec** is what declares the intent, the where, when and why.
It is like building a house, the spec is the blueprint.

With this Architecture is no longer advisory; it is executable and enforceable.

For those reasons the SDD has a Workflow:

1) **Specify:** Define 'what' the software should do in a functional specification.
2) **Plan:** Create the technical architecture and break it down into tasks.
3) **Implement:** The AI generates code for each task, guided by the spec and plan.
4) **Validate:** Verify the generated code against the original specification.

### Benefits:
This becomes the AI Predictable, I will know what the AI will build before it writes any code. Also it gives Traceability of  what we do, linking every piece of logic back to a specific requirement. Avoiding Errors catching misalignments and errors early in the process. Finally it Improves Quality, clear specs and small tasks lead to better AI code, also this allow to self-maintain Docs, because any change of the docs that is not up to date will cause the build fails.

- **Predictability**: Know what the AI will build before it writes any code.
- **Traceability**: Link every piece of logic back to a specific requirement.
- **Error Prevention**: Catch misalignments and errors early in the process.
- **Self-Maintaining Docs**: Documentation stays current or builds fail.
- **Improved Quality** Clear specs and small tasks lead to better AI Code.
## Golden rule
Use the minimum rigor needed to remove ambiguity for your project.

## Human in the loop
In SDD, the human role shifts from "coder" to "Architect" and "governor". The protocol demands that humans review and validate the Specification and Plan, rather than just debugging the downstream code. This ensures that human judgment is applied to intent, policy, and ethics, while the machine handles the mechanical labor of execution.

## Spectrum of spec:
- **Spec First:** Spec guides - Initial code.
- **Spec-Anchored**: Spec is 'living documentation' - Production systems
- **Spec as only source:** Humans only edit the spec - Embedded systems

## Files and Figures used in SDD

-  Project constitution
-  [[Skills]]
-  Human in the loop