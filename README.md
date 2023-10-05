# Rust Code Review Guidelines

- [中文](./README-ZH.md)

[Rust Code Review Guidelines](https://github.com/ZhangHanDong/rust-code-review-guidelines) (RCRG) invites everyone to participate in its maintenance and improvement, aiming for higher quality Rust code.

## Introduction

The engineering quality of software systems is related to various factors, such as code readability, maintainability, performance, etc., which require our comprehensive consideration.

Although the powerful Rust compiler can ensure memory safety of Rust code at compile time, it has its limitations. This is under the premise that you've prohibited Unsafe Code and written entirely in Safe Rust. Even with Safe Rust, in concurrent scenarios, there are risks of deadlocks and data races due to improper memory order specifications in lockfree scenarios. Even if memory safety is ensured, the entire system may still have security risks.

Relying solely on the Rust compiler, rustfmt, clippy, and other tools is not enough to guarantee the best engineering quality. Therefore, in actual development, to ensure the engineering quality of the entire system code, a set of code review standards is essential. Ideally, there should be a code review checklist for reviewers to efficiently review code, and even establish a standard for future AI code reviews.

## Rust Code Review Checklist:

- **Correctness**
	- Ensure the code compiles without warnings. Fix or document any warnings.
	- Check the business logic to ensure no errors or edge cases are overlooked.
	- Verify appropriate error handling.
	- Ensure Unsafe code is correct and accompanied by standard documentation. Further reference safety.
- **Readability**
	- Ensure the code is easy to read and understand.
	- Check for clear and descriptive naming, and consistent style and formatting.
	- Verify comments explain intentions and complex parts.
	- Ensure code is reasonably organized into functions and modules.
- **Maintainability**
	- Check for duplicated logic and consider consolidation.
	- Identify parts that can be abstracted into generic, reusable components.
	- Look for improperly abstracted or overly complex situations.
	- Ensure tests cover key paths and edge cases.
	- Verify documentation comments explain implementation details.
	- Check if the code structure is logical and adheres to principles like Single Responsibility and Open/Closed.
	- Examine code architecture coupling.
- **Safety (Unsafe Safety & Security)**
	- Ensure safety abstractions of Unsafe code are standard and reasonable, especially at FFI boundaries.
	- Identify potential vulnerabilities like buffer overflows and SQL injections.
	- Suggest input validation and filtering methods.
	- Look for static conditions in concurrent scenarios, improper synchronization, and data race risks due to improper memory order specifications in lockfree or Unsafe code scenarios.
	- Ensure proper authentication and authorization.
	- Ensure supply chain security, verify the reliability and safety of external libraries, and avoid using deprecated or long-unupdated libraries.
- **Performance**
	- Identify obvious inefficiencies, such as unnecessary memory allocations.
	- Suggest better data structures or algorithms where applicable.
	- Point out areas that can be optimized through lazy evaluation, asynchronous processing, or parallelism.
	- Ensure there are sufficient performance benchmarking documents before performance optimization to prevent performance regression.
    - Balance compilation size, compilation time, and performance optimization based on actual scenarios.
- **API Design**
	- Consider the consistency, intuitiveness, and potential usability issues of the API.
	- Suggest improvements to API naming, interfaces, and documentation.
	- Point out unclear or missing parts of API behavior.
	- Identify risks exposed by Unsafe code.
- **Debuggability**
    - Logging: Ensure there's adequate logging, especially in critical paths and potential error points. Logs should be clear, meaningful, and help developers quickly pinpoint issues.
    - Error Messages: Ensure error messages are clear, specific, and provide enough context to help locate issues.
    - Assertions and Verifications: Use assertions at key points to verify assumptions, ensuring code behavior is as expected.
    - Documentation and Comments: Ensure complex code sections have sufficient comments and documentation to help other developers understand how they work.
- **Observability**
    - Monitoring and Metrics: Ensure code integrates with monitoring tools and has adequate metrics to monitor system health and performance.
    - Tracing: If the application is distributed, ensure it integrates with distributed tracing tools like OpenTelemetry to help trace requests through the system.
    - Alerts: Ensure appropriate alert thresholds and notification mechanisms are set up to notify relevant personnel promptly when issues arise.
    - Health Checks: For services and applications, ensure there are health check endpoints for monitoring tools and load balancers to check their health.
- **Others**
	- If the code needs to run on multiple platforms, ensure cross-platform compatibility is considered.
	- Ensure the code can be compiled and tested normally in a CI/CD environment.

## Call for Contributions

The current Rust Code Review Guidelines is just a draft. To refine it, everyone's participation is needed. In the future, we need to establish more detailed standards and scoring systems for each review dimension, as well as corresponding code examples, primarily based on projects in the Rust open-source ecosystem. This requires everyone's collective participation.