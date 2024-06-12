# Vecto

Hybrid Search with Postgres and Ecto

Loosely based on:
- https://github.com/pgvector/pgvector-python/blob/master/examples/hybrid_search_rrf.py
- https://github.com/Azure-Samples/rag-postgres-openai-python/blob/e30ea96ca11ca6578ca38d3428594bd98d704900/src/fastapi_app/postgres_searcher.py#L2
- https://supabase.com/docs/guides/ai/hybrid-search
- https://github.com/toranb/rag-n-drop/blob/main/lib/demo/section.ex#L30

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `vecto` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:vecto, "~> 0.1.0"}
  ]
end
```

## Setup

1. Create a tsvector column in your table (postgres "generated" column recommended based on one or combo of text columns)
2. Create a GIN index on the tsvector column
3. Create a HNSW Cosine distance [index](https://github.com/pgvector/pgvector?tab=readme-ov-file#hnsw) on the vector column
4. Generate embeddings for your documents and store them in the vector column (e.g. using BERT via [Bumblebee](https://github.com/elixir-nx/bumblebee), OpenAI's API, etc)
4. Generate embeddings for your search query and pass to query_embedding

### Usage

```
Blog
|> Vecto.hybrid_search([0.11, 0.03, -0.02, ...], "what is a cat")
|> Repo.all()
```

### TODO

- Tests!
- Implement additional vector search functions (e.g. cosine similarity, euclidean distance)
- Allow for different tsquery options.

Docs can be found at <https://hexdocs.pm/vecto>

