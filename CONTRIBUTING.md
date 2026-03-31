# Contributing to the Enterprise AI Constitution Standard

Thank you for your interest in contributing. This is an open standard — it improves through real-world use and community input.

---

## Ways to Contribute

### Report issues
If you've deployed a constitution and found a gap, edge case, or ambiguity in the standard, open an issue describing:
- What section is affected
- What scenario exposed the gap
- What behavior you expected vs. what occurred

### Propose changes to the standard
1. Fork the repository
2. Create a branch for your change
3. Edit the relevant section(s) in `standard/`
4. Submit a pull request with a clear description of:
   - What you changed and why
   - Whether this was informed by real-world deployment experience
   - Any trade-offs or considerations

### Add examples
We welcome anonymized examples of constitutions deployed in production. Place them in `examples/` and ensure:
- No real company names, employee names, or identifying details
- Regulatory frameworks and industry context are preserved (these are what make examples useful)
- A brief header explains the organization type and what makes this example notable

### Add test cases
If you've identified scenarios not covered by the existing test suite, add them to `tests/`. Each test case should include:
- The section being tested
- The prompt used
- Expected behavior
- Why this scenario matters

### Improve documentation
Clarifications, deployment guides, and integration examples in `docs/` are always welcome.

---

## What We're Not Looking For

- Product pitches or vendor-specific integrations
- Changes that make the standard less general (more restrictive for a specific industry without clear rationale)
- Theoretical additions not grounded in deployment experience

---

## Style Guidelines

- Write in clear, direct prose. Avoid jargon where a plain word works.
- The standard is addressed to the AI, not to the reader. Sections in `standard/` should maintain second-person address ("You are...", "You must...").
- Templates use `{{placeholder}}` syntax for fill-in fields.
- Keep examples concrete. "Do not transmit Tier 2 data to personal accounts" is better than "exercise caution with sensitive information."

---

## License

By contributing, you agree that your contributions will be licensed under the same [CC BY 4.0](LICENSE) license that covers this project.
