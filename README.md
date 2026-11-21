## Hi, I'm Marcel Good

I'm a software architect and hands-on technical lead, and a partner at [IdeaBlade](https://www.ideablade.com). For the past 16 years I've been designing, building and modernizing business-critical applications for clients. Over 25 years in software overall, including leading a 20+ person technology organization.

- **What I work in:** C# and .NET (ASP.NET Core), TypeScript with Angular and React, SQL Server and PostgreSQL, Microsoft Azure, CI/CD with GitHub Actions and Azure DevOps.
- **Angular from the start:** I was part of the IdeaBlade team Google engaged during the Angular 2 beta for enterprise-development feedback; IdeaBlade wrote Angular's original documentation, and we validated it by building real applications on the beta.
- **Modernization:** moving established .NET Framework, desktop and client-server applications onto modern .NET and Angular, one step at a time, with automated tests in CI.
- **AI in business applications:** we're working with clients at IdeaBlade on early-stage AI projects, and I build in public to try ideas and measure what works. I use Claude Code every day: TempHire and its React version were built with it, with me directing the work and reviewing and testing every change before it's merged. I also used it to extract IdeaBlade Validation, which I wrote by hand in three projects over several years, into a standalone library.

### Modernization showcase: [TempHire](https://github.com/Breeze/temphire.angular)

I wrote IdeaBlade's [Punch](https://github.com/IdeaBlade/Punch) framework for data-driven XAML apps (Caliburn.Micro + DevForce + Entity Framework). Its TempHire reference app started out in Silverlight and WPF. I've rewritten it as a modern line-of-business web app: **Angular 22** (standalone, zoneless, signals) with Optimus UI (the open-source fork of PrimeNG), **Breeze 3**, **ASP.NET Core 10** and **EF Core 10**. Every ported file names the file it came from, and the conversion notes map the old architecture onto the new one, so it doubles as a guide for migrating legacy .NET desktop apps to the web.

It also goes beyond the original:

- **One set of validation rules for client and server**, written once on the server and enforced in the browser as you type and again on save, with [IdeaBlade Validation](https://github.com/Breeze/ideablade-validation) (below).
- **Multi-tenant:** EF Core global query filters, with the tenant carried in the access token.
- **Modern security:** the original kept users in a table of its own; TempHire uses **ASP.NET Core Identity** with Editor and Reader roles, and the server is its own **OAuth 2.1** authorization server, built with OpenIddict. The app signs in with the Authorization Code flow and PKCE and never sees a password, and every endpoint declares who may call it.
- **Quinn, an AI assistant** that answers questions about the staffing data, built in .NET with Microsoft.Extensions.AI and an MCP server built with the MCP C# SDK, on a local Ollama model or Claude. The agent calls its tools as the signed-in user, so it only ever sees that user's company's data, and its answers stream as the model writes. The MCP server follows the MCP authorization spec, so an MCP client such as Claude Code needs nothing but the URL.
- **Quinn's budgets:** every answer from a paid model costs money, so usage is tracked in tokens and dollars, with daily, weekly and monthly budgets per user and per company. A usage page shows where everyone stands, and Quinn says which budget ran out and when it starts over. A typical question costs about $0.013 on Claude Sonnet 5.5.

**The server now has a repository of its own: [temphire.server](https://github.com/Breeze/temphire.server).** It's shared by both clients as a git submodule, and its README documents the server, Quinn and the budgets.

**Now also in React: [temphire.react](https://github.com/Breeze/temphire.react).** For teams weighing a move from Angular to React, I've converted TempHire again: **React 19** with Mantine, React Router and Vite, on the same Breeze 3 and .NET server, with the same screens and behaviour. Every file names its Angular counterpart, and a guide to React for Angular developers maps the concepts side by side, from signals and dependency injection to hooks and context, with examples from both versions.

### Validation framework: [IdeaBlade Validation](https://github.com/Breeze/ideablade-validation) (preview)

Most applications tie validation to their forms, so the rules for one entity end up spread across every screen that edits it, and they drift apart. IdeaBlade Validation puts the rules with the data: they live in one JSON metadata structure that the browser and the server share, and much of it comes from the server model for free (a `varchar(255)` column becomes a 255-character limit everywhere).

- **TypeScript and .NET**, with matching implementations; a shared conformance suite runs in both the Vitest and xUnit test suites, so the two can't drift apart. The .NET library targets .NET Standard 2.0, .NET 8 and .NET 10.
- **Sync and async validators**, plugged in by name through dependency injection, and **continuous validation** of whole entity stores, so errors show wherever they matter, not only in forms.
- **No `eval`:** conditions run in a sandboxed expression interpreter that works under a strict Content Security Policy, with one grammar on both platforms.
- **Angular** (signals, reactive, template-driven and Signal Forms) and **React** (hooks) integrations, and a ready-made **Breeze 3** integration built only on public extension points, so any data layer can plug in.

TempHire uses it in both versions. The packages aren't on npm or NuGet yet.

### AI showcase: [rag-example](https://github.com/marcelgood/rag-example)

A step-by-step reference implementation in TypeScript/Node.js, where every change is measured by evals:

1. RAG over documents, with cited answers
2. Questions over a relational database (text-to-SQL)
3. Evals: graded test questions to compare each change
4. The database tools as an MCP server
5. The tool loop with the Vercel AI SDK
6. Sign-in and per-company data isolation
7. Hybrid search and re-ranking with LangChain retrievers

One result: re-ranking raised first-place retrieval accuracy from 60% to 88%, while hybrid search didn't beat plain keyword search. The measurements decided what stayed.

### Open source

I'm part of the IdeaBlade team behind the [Breeze](https://github.com/Breeze) data management libraries, BreezeJS for JavaScript/TypeScript and BreezeSharp for .NET, used by companies around the world, including [Breeze 3](https://github.com/Breeze/breeze-client-v3), the ESM rewrite for modern TypeScript released in 2026, and the [Breeze .NET server](https://github.com/Breeze/breeze-server-v3) for ASP.NET Core and EF Core.

### Connect

[LinkedIn](https://www.linkedin.com/in/marcelgood)
