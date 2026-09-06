# Semantic-Cache-for-LLM-Cost-Control

What it is: A service that sits in front of an LLM API and remembers answers to questions it's already seen — even reworded ones — so it doesn't pay for or wait on the same answer twice.

Why: The same question gets asked in different words all the time. Exact-match caching misses almost all of that overlap. This one matches by meaning instead.

How it works: Incoming question → turned into a vector → compared against past questions. Close enough match → saved answer returned instantly, no LLM call. New question → LLM is called as normal, then it's saved for next time.

Stack: FastAPI (backend) · FAISS (similarity search) · SQLite (stores cached answers) · tiktoken (cost tracking) · pytest (tests) · Docker (packaging)

Result: 37% of repeat questions caught in testing, answered in ~2ms instead of ~600ms for a real call.
