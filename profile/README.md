# Indx Search System

**Indx** is a high-performance, typo-tolerant search engine for **.NET**. It matches at the character-pattern level rather than through tokenizers and per-language stemmers, so typos, inflections, compound words and messy input are handled without language configuration.

Run it as a server, or embed the library directly in your application. No clusters, no analyzers, no operational overhead.

**[Try the live demo](https://www.indx.co)**

---

## Run the server

[**Indx**](https://github.com/indxSearch/Indx) is a complete, self-hosted search server. Clone it and run:

```bash
git clone https://github.com/indxSearch/Indx
cd Indx
dotnet run
```

Open `https://localhost:5001`. The first visit creates your admin account and team, and takes under a minute. Nothing else to configure: SQLite databases are created for you, and email goes to the console until you set up a provider.

Requires the [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0).

**Ready to deploy on Azure App Service**: zip deploy the published output, turn on WebSockets for the console, and there is nothing else to provision. It runs the same on any host that gives it .NET 10, a persistent disk and a long-lived process, so a VPS, Fly.io, Render or an EC2 instance all work. Search indexes live in memory and the databases are SQLite files on local disk, so it wants one instance with room rather than several small ones.

**What you get**

- **Console** for teams, datasets, field configuration, search preview, boost rules and synonyms
- **Statistics** for every dataset: what people search for, which results they choose, and the misspelled searches fuzzy search still answered
- **HTTP API** with JWT authentication and scoped API keys, documented in Swagger at `/swagger`
- **MCP server** at `/mcp`, so AI agents can search your data directly
- **Dynamic data**: insert, update and delete by key or by filter, with the index kept in sync
- **Zero-downtime rebuilds**: replace a dataset or change its field configuration on a shadow engine while the old one keeps serving
- **Relevance tools**: boost rules with schedules, facets, coverage, vector and hybrid search
- **SQLite storage**, so there is no external database to run

Indx Server v2 is in beta, built on the stable IndxSearchLib 5.0. See the [documentation](https://v5.docs.indx.co).

---

## Or embed the library

The same engine as a C# class library, with no server involved. Point it at your JSON, mark a few fields as searchable, and search.

```csharp
using Indx.Api;
var engine = new SearchEngine();

FileStream stream = File.Open("movies.json", FileMode.Open, FileAccess.Read);
engine.Init(stream);

engine.GetField("title")!.Searchable = true;
engine.GetField("description")!.Searchable = true;

engine.Load(stream);
engine.Index();

var result = engine.Search(new Query("matrix", 10));
```

`IndxSearchLib` 5.0 on [NuGet](https://www.nuget.org/packages/IndxSearchLib). This snippet compiles unchanged on v4 and v5. The APIs do differ elsewhere, so see the [migration guide](https://github.com/indxSearch/skill-indx-search/blob/main/references/migration-v4-to-v5.md) if you are upgrading.

---

## What makes Indx different

- **A different matching model**  
  Fragments of similar structure match, where shape and length influence recognition. There is no tokenizer to tune and no stemmer per language.

- **Relevance across whole strings**  
  Indx ranks against entire strings, so it weighs how terms relate to one another rather than only whether they are present.

- **Nothing to configure**  
  No analyzers, no schemas, no stop words, no stemming rules. Index your data and search it.

---

## Documentation and tooling

- **[Documentation](https://v5.docs.indx.co)** for Indx 5. Still on v4? Its documentation is at [docs.indx.co](https://docs.indx.co), and the [migration guide](https://github.com/indxSearch/skill-indx-search/blob/main/references/migration-v4-to-v5.md) takes you to v5.

- **[Agent skill](https://github.com/indxSearch/skill-indx-search)** teaches your coding agent Indx concepts, integration and search UX patterns.
  ```bash
  npx skills add indxSearch/skill-indx-search
  ```

## Repositories

| Repository | What it is |
|---|---|
| **[Indx](https://github.com/indxSearch/Indx)** | The search server. Console, HTTP API, MCP, statistics, authentication and user management. |
| **[skill-indx-search](https://github.com/indxSearch/skill-indx-search)** | Agent skill for Indx. |
| **[indx-react](https://github.com/indxSearch/indx-react)** | React UI kit for building search interfaces: components, tools and types. |

---

### Learn more

- https://indx.co
- https://v5.docs.indx.co
