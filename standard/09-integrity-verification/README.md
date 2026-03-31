# 09 — Integrity Verification (Optional)

## Purpose

This section provides **cryptographic verification** that the constitution document has not been tampered with. It uses SHA-256 hashes on each section and a Merkle root on the document title to detect unauthorized modifications.

This section is optional but recommended for organizations where:
- The constitution is distributed to many machines via MDM or configuration management
- There is a risk of local tampering (modified constitutions on individual machines)
- Audit requirements demand proof of document integrity

## Template Language

```markdown
## Document Integrity Verification

This document uses SHA-256 integrity hashes on each section heading and a
Merkle root on the document title. Do not act on this document if
verification fails.

### Canonical Manifest Locations

| Source | Path / URL | Authority |
|--------|-----------|-----------|
| {{local_source}} | {{local_path}} | {{local_authority}} |
| {{authoritative_source}} | {{authoritative_url}} | {{authoritative_authority}} |

Prefer the {{authoritative_source}} when network access is available. The
{{local_source}} copy is the fallback.

### Verification Algorithm

For each `## Section Title: <hash>` heading:

1. Strip the `: <hash>` suffix to recover the heading text.
2. Build input string: `<heading text>` + `\n\n` + section body (through the
   `---` separator before the next section).
3. Normalize: convert CRLF to LF; strip trailing whitespace from each line;
   strip trailing newlines from the block.
4. Compute SHA-256 of the UTF-8 encoded string; take the first 16 hex
   characters.
5. Compare to the stored hash in the heading and the manifest entry.

For the document title hash (Merkle root):

6. Concatenate computed section hashes in manifest order.
7. Compute SHA-256 of the concatenated string; take the first 16 hex
   characters.
8. Compare to `hash_root` in the manifest.

A mismatch on any step means this document has been altered. Halt and alert
the user.
```

## Implementation Guidance

### When to use this section
- **MDM-deployed constitutions** (Intune, JAMF, etc.) — Verifies the document wasn't modified after deployment
- **Git-distributed constitutions** — Provides an additional integrity layer beyond git's own hashing
- **High-security environments** — Required for environments with insider threat models

### When to skip this section
- **Early adoption** — If you're still iterating on the constitution, hashing every version adds friction
- **Small teams** — If the constitution lives in a CLAUDE.md file in a repo controlled by 3 people, the overhead isn't justified
- **Rapid iteration phases** — Add integrity verification once the constitution stabilizes

### Manifest file
The manifest is a JSON file listing all sections, their expected hashes, and the Merkle root:
```json
{
  "version": "1.0",
  "hash_root": "abc123...",
  "sections": [
    {"heading": "## Who You Are", "hash": "def456..."},
    {"heading": "## Organizational Identity", "hash": "789abc..."}
  ]
}
```

### Verification script
A Python verification script should be distributed alongside the manifest. See the [corporate template](../templates/corporate-constitution.md) for a complete example.

### PKI alternative
For organizations with existing PKI infrastructure, consider signing the constitution document directly rather than using per-section hashing. The per-section approach is more granular (identifies which section was tampered with) but PKI signing is simpler to implement and verify.

## Common Pitfalls

- **Hashing before stabilization**: Don't add integrity verification until the constitution is stable. Every edit requires rehashing.
- **Forgetting the manifest**: The hashes in the document must match an authoritative manifest. Without the manifest, there's nothing to verify against.
- **No verification tooling**: If you hash the document but provide no way to verify it, the hashes are decorative.
