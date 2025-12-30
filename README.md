# Fuzzy Spoon

Fuzzy Spoon is a lightweight, high-performance fuzzy matching library and toolkit that makes approximate-string matching and smart suggestions simple and reliable. Built for real-world UX needs, Fuzzy Spoon focuses on speed, friendly defaults, and easy integration so you can add typo-tolerant search, autocompletion, and intelligent ranking to CLI tools, web apps, editors, and backend services with minimal effort.

Why Fuzzy Spoon?

- Robust fuzzy matching that tolerates typos, transpositions, and partial input.
- Fast and memory-efficient: designed for large lists and real-time use.
- Configurable scoring and ranking to prioritize the results that matter.
- Small API surface and flexible adapters to plug into UI components, command palettes, and search endpoints.

Core features

- Fuzzy matching algorithm with adjustable sensitivity and penalty tuning.
- Incremental / streaming search for responsive autocompletion.
- Multi-field and weighted matching for records with names, tags, and metadata.
- Result scoring and stable ranking across repeated queries.
- Simple adapter pattern for integration with front-end components or back-end services.

Quick highlights

- Audience: developers building search, suggestions, or fuzzy lookup features.
- Goal: deliver fast, accurate, and configurable fuzzy matching with minimal engineering overhead.
- Outcome: improved UX for search/autocomplete, fewer missed matches, and predictable ranked results.

Installation

Install from npm (JavaScript/TypeScript):

npm install fuzzy-spoon

or via pip (Python wrapper):

pip install fuzzy-spoon

(If using the native library directly in another language, see the language integration section.)

Quick start

JavaScript (Node.js)

const { FuzzySpoon } = require('fuzzy-spoon');

const fs = new FuzzySpoon({
  sensitivity: 0.8,
  transpositionPenalty: 0.9,
});

const items = ['apple', 'apricot', 'banana', 'grape', 'pineapple'];
const results = fs.search('appel', items, { maxResults: 5 });
console.log(results);

Python

from fuzzy_spoon import FuzzySpoon

fs = FuzzySpoon(sensitivity=0.8, transposition_penalty=0.9)
items = ['apple', 'apricot', 'banana', 'grape', 'pineapple']
results = fs.search('appel', items, max_results=5)
print(results)

CLI

# interactive fuzzy search on a newline-separated file
fuzzy-spoon find --file items.txt --query "appel" --top 5

API overview

- Constructor / initializer
  - sensitivity: number (0.0 - 1.0) — how permissive the matcher is.
  - transpositionPenalty: number — penalty multiplier for transposed characters.
  - fieldWeights: object — per-field weights when matching multi-field records.

- search(query, items, options)
  - query: string — user input to match.
  - items: array|string — list of strings or records to match against.
  - options: { maxResults, minScore, fields } — controls result size and filtering.
  - returns: array of { item, score, highlights }

- stream(query)
  - Returns an async iterator or observable for incremental results (useful for very large sets or streaming sources).

Configuration and tuning

- Sensitivity governs how permissive matches are. Lower values make matching stricter.
- Field weights boost matches where important fields (e.g., title) should outrank less important fields (e.g., tags).
- You can combine fuzzy and exact matching by using minScore and exact-match boosts.

Performance and benchmarks

Fuzzy Spoon is optimized for low-latency lookups. Typical benchmarks (on commodity hardware):

- 10k short strings: average search < 5ms
- 100k short strings: average search 20–30ms (depends on configuration)

Exact performance depends on dataset, average string length, and tuning parameters. If you need specialized indexing (trie, n-gram, or precomputed embeddings), Fuzzy Spoon provides adapter hooks for custom indexes.

Examples

- Command palette: integrate Fuzzy Spoon in an editor/IDE to provide instant fuzzy search of commands and files.
- Autocomplete: incremental search as the user types, returning top-k ranked suggestions.
- Deduplication: fuzzy record linkage across name and address fields using multi-field scoring.

Roadmap

- Add first-class fuzzy indexes (n-gram/trie) for extremely large datasets.
- Native bindings for more languages and runtime-specific optimizations.
- Prebuilt adapters for popular UI libs (React, Svelte, Vue) and server frameworks.

Contributing

We welcome contributions! Please read CONTRIBUTING.md for details. Typical contribution workflow:

- Fork the repository
- Create a feature branch
- Add tests for new behavior
- Open a PR with a clear description and reference to any related issues

Maintainability

- Tests: run npm test (or pytest for Python wrappers)
- Linting: eslint (JS) and flake8 (Python) recommended
- CI: the project uses GitHub Actions. Ensure new changes pass CI.

License

MIT — see the LICENSE file for details.

Security

If you discover a security vulnerability, please do not open a public issue. Contact the maintainers directly or use the security policy if provided.

Contact

Maintainer: brenticusbaked

Acknowledgments

Inspired by other fuzzy matchers and UX-focused search tools. Thanks to contributors and users who help improve the library.
