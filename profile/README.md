# Indx Search System

**Indx** is a free, high-performance, enterprise-ready, embeddable search engine for **.NET**.

It delivers **the fastest search performance on the market** without requiring servers, clusters, or operational overhead.

Indx is designed to drop in and just work — whether you're building a SaaS platform, a high-throughput service, or a lightning-fast local application.

 **[View live demo here](https://www.indx.co)**

---

### Get started

| Using C# Class Library | Deploying a server |
|------------------------|-------------------|
| **Install via NuGet**<br>`dotnet add package IndxSearchLib`<br>[Package details →](https://www.nuget.org/packages/IndxSearch)<br><br>A full enterprise search system in a class library | **Deploy HTTPS API template**<br>`git clone https://github.com/indxSearch/IndxCloudApi`<br>[View repository →](https://github.com/indxSearch/IndxCloudApi)<br><br>Production-ready with Blazor UI, HTTP API, authentication, and user management. |


### What makes Indx different?

- **A fundamentally better matching model**  
  Indx uses pattern recognition rather than a lexical model. It matches fragments of similar structure, where shape and length influence recognition — enabling robust matching across variations.

- **Relevancy ranking**  
  Indx matches entire strings, allowing it to understand relationships between terms — not just their presence.

- **Zero-configuration by design**  
  Indx has no analyzers, schemas, or language-specific tuning. There are no stop words, no stemming rules, and no tokenizer configuration. You index data and search it — that’s it.

Together, this makes Indx less like a traditional search engine and more like a precision instrument for structured, high-performance search.

---

### Index and search in a few lines of C#

Point Indx at your JSON, mark a few fields as searchable, and run your app.

```C#
using Indx.Api;
var engine = new SearchEngine();

// ANALYZE AND INDEX JSON
FileStream fstream = File.Open("movies.json", FileMode.Open, FileAccess.Read);
engine.Init(fstream);

engine.GetField("title")!.Searchable = true;
engine.GetField("description")!.Searchable = true;

engine.Load(fstream);
engine.Index();

// SEARCH
var result = engine.Search(new Query("matrix", 10));
```

### Learn more

- 🌐 https://indx.co  
- 📘 https://docs.indx.co
