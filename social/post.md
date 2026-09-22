Wired a Compact Knowledge Graph into Strands.

“Show prerequisites of thread_id.”

Local CKG lookup. No model call. About 0.1 ms.*

“Explain the prerequisites of thread_id.”

Strands gets the same declared edges and generates an explanation. One model call.

The useful part: the application knows when a graph lookup is enough. Those requests never start the model loop.

Small experiment. Working integration. A practical boundary between retrieval and generation.

Project overview and reported results:
https://github.com/Yarmoluk/ckg-strands-showcase

The implementation and full CKG remain private.

*Local request processing only; excludes graph loading, Python startup, and printing. One example per route; different tasks, not a speed comparison.

#ContextEngineering #KnowledgeGraphs #AIAgents #StrandsAgents
