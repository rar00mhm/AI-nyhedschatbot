import React, { useEffect, useMemo, useRef, useState } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { Send, Loader2, User, Bot, LogIn, Search } from "lucide-react";
import { Button } from "@/components/ui/button";
import { Card } from "@/components/ui/card";
import { Textarea } from "@/components/ui/textarea";
import { cn } from "@/lib/utils";

/**
 * RKV 2025 — Hej‑style Chatbot UI (single file)
 * -------------------------------------------------
 * This file previously threw: "Identifier 'React' has already been declared".
 * Cause: the file content (including the React import) existed twice.
 * Fix: remove the duplicate block and keep a single import/component set.
 *
 * Backend endpoints to wire:
 * - POST /api/ask { query, topK, lang, model } -> { answer, sources, usage }
 * - POST /api/ingest (FormData files[]) -> { count }
 */

/** Utility: sanitize a user query before sending */
export function sanitizeQuery(q: string): string {
  return q.replace(/\s+/g, " ").trim();
}

export type Source = { title: string; url?: string; snippet?: string };
export type Usage = { promptTokens?: number; completionTokens?: number; totalTokens?: number };
export type Msg = { id: string; role: "user" | "assistant"; content: string; sources?: Source[]; usage?: Usage; ts?: number };

export default function RKVHej() {
  const [messages, setMessages] = useState<Msg[]>([]);
  const [input, setInput] = useState("");
  const [loading, setLoading] = useState(false);
  const [model] = useState("gpt-5-thinking");
  const [topK] = useState(5);
  const endRef = useRef<HTMLDivElement | null>(null);

  useEffect(() => { endRef.current?.scrollIntoView({ behavior: "smooth" }); }, [messages]);

  const suggested = useMemo(() => (
    [
      { t: "Hvordan stemmer jeg til valget?", e: "⚡" },
      { t: "Hvad er status på kommunens budget?", e: "🏛️" },
      { t: "Hvad betyder ændringerne i dagpengene?", e: "💬" },
    ]
  ), []);

  async function handleAsk(q?: string) {
    const query = sanitizeQuery(q ?? input);
    if (!query) return;
    setInput("");
    const uMsg: Msg = { id: crypto.randomUUID(), role: "user", content: query, ts: Date.now() };
    setMessages(m => [...m, uMsg]);
    setLoading(true);
    try {
      const res = await fetch("/api/ask", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ query, topK, model })
      });
      if (!res.ok) throw new Error("/api/ask failed");
      const data = await res.json();
      const aMsg: Msg = {
        id: crypto.randomUUID(),
        role: "assistant",
        content: data.answer ?? "(Tomt svar)",
        sources: data.sources ?? [],
        usage: data.usage ?? {},
        ts: Date.now()
      };
      setMessages(m => [...m, aMsg]);
    } catch (e: any) {
      setMessages(m => [...m, { id: crypto.randomUUID(), role: "assistant", content: `Der skete en fejl: ${e?.message ?? e}`, ts: Date.now() }]);
    } finally { setLoading(false); }
  }

  return (
    <div className="min-h-screen flex flex-col bg-white">
      <TopBar />

      {/* Hero / Logo + tagline */}
      <section className="relative mx-auto w-full max-w-5xl px-4 pt-10">
        <div className="flex flex-col items-center text-center">
          <div className="flex items-center gap-3 mb-2">
            <div className="h-12 w-12 rounded-full bg-yellow-300 grid place-items-center text-black text-2xl">🙂</div>
            <div className="text-4xl font-extrabold leading-none">Hej</div>
            <div className="ml-1 text-xl font-semibold tracking-tight">RKV 2025</div>
          </div>
          <p className="text-slate-600 max-w-2xl">Stil spørgsmål om RKV’s journalistik og få AI‑genererede svar. Svarene bygger på jeres egne artikler og kilder.</p>
        </div>

        {/* Suggested question tiles */}
        <div className="mt-6 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3 place-items-stretch">
          {suggested.map((s, i) => (
            <motion.button
              key={i}
              onClick={() => handleAsk(s.t)}
              className="text-left rounded-2xl border px-3 py-3 shadow-sm hover:shadow transition bg-white"
              whileHover={{ y: -1 }}
            >
              <div className="text-sm flex items-start gap-2">
                <span className="text-lg leading-none select-none">{s.e}</span>
                <span>{s.t}</span>
              </div>
            </motion.button>
          ))}
        </div>
      </section>

      {/* Chat history */}
      <main className="mx-auto w-full max-w-5xl px-4 mt-6 flex-1">
        <div className="min-h-[30vh]">
          <div className="flex flex-col gap-4 pb-40">
            {messages.map(m => (
              <AnimatePresence key={m.id}>
                <motion.div initial={{ opacity: 0, y: 8 }} animate={{ opacity: 1, y: 0 }} exit={{ opacity: 0, y: -8 }}>
                  <Message msg={m} />
                </motion.div>
              </AnimatePresence>
            ))}
            {loading && (
              <div className="flex items-center justify-center gap-2 text-sm text-slate-500"><Loader2 className="h-4 w-4 animate-spin"/> Genererer svar…</div>
            )}
            <div ref={endRef} />
          </div>
        </div>
      </main>

      {/* Bottom composer like Aftonbladet */}
      <div className="sticky bottom-0 w-full bg-white/90 backdrop-blur border-t">
        <div className="mx-auto max-w-3xl px-4 py-4">
          <Card className="p-2 rounded-full shadow-sm">
            <div className="flex items-center gap-2">
              <Textarea
                value={input}
                onChange={(e) => setInput(e.target.value)}
                placeholder="Skriv dit spørgsmål her"
                className="border-0 focus-visible:ring-0 resize-none rounded-full h-12 py-3 px-5"
                onKeyDown={(e) => {
                  if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    handleAsk();
                  }
                }}
              />
              <Button onClick={() => handleAsk()} disabled={loading || !input.trim()} className="h-12 rounded-full px-5">
                {loading ? <Loader2 className="h-4 w-4 animate-spin"/> : <Send className="h-4 w-4"/>}
              </Button>
            </div>
          </Card>
          <div className="text-center text-xs text-slate-500 mt-2">
            <a className="inline-flex items-center gap-1 hover:underline" href="#login"><LogIn className="h-3 w-3"/> Log ind for at stille egne spørgsmål</a>
          </div>
        </div>
      </div>
    </div>
  );
}

function Message({ msg }: { msg: Msg }) {
  const isUser = msg.role === "user";
  return (
    <div className={cn("flex gap-3", isUser ? "justify-end" : "justify-start") }>
      {!isUser && <div className="h-8 w-8 rounded-full bg-yellow-300 text-black grid place-items-center"><Bot className="h-4 w-4"/></div>}
      <div className={cn("max-w-[80%] rounded-2xl p-4 shadow-sm", isUser ? "bg-slate-900 text-white" : "bg-slate-50 border") }>
        <div className="prose prose-sm max-w-none whitespace-pre-wrap">{msg.content}</div>
        {msg.sources && msg.sources.length > 0 && (
          <div className="mt-3 border-t pt-2">
            <div className="text-[10px] uppercase tracking-wide mb-1 text-slate-500">Kilder</div>
            <ul className="space-y-2">
              {msg.sources.map((s: Source, i: number) => (
                <li key={i} className="text-xs">
                  <div className="font-medium leading-tight">{s.title}</div>
                  {s.snippet && <div className="text-slate-500 leading-snug">{s.snippet}</div>}
                  {s.url && <a href={s.url} className="underline" target="_blank" rel="noreferrer">{s.url}</a>}
                </li>
              ))}
            </ul>
          </div>
        )}
      </div>
      {isUser && <div className="h-8 w-8 rounded-full bg-slate-200 text-slate-700 grid place-items-center"><User className="h-4 w-4"/></div>}
    </div>
  );
}

function TopBar() {
  return (
    <div className="w-full bg-[#e30613] text-white">
      <div className="mx-auto max-w-6xl px-4 h-10 flex items-center gap-5">
        <div className="font-extrabold tracking-tight">RKV</div>
        <nav className="hidden md:flex items-center gap-4 text-sm">
          <a className="hover:underline" href="#">Start</a>
          <a className="hover:underline" href="#">Sport</a>
          <a className="hover:underline" href="#">Nyheder</a>
          <a className="hover:underline" href="#">Kultur</a>
          <a className="hover:underline" href="#">Ledere</a>
          <a className="hover:underline" href="#">Hej</a>
        </nav>
        <div className="ml-auto flex items-center gap-3 text-sm">
          <button className="inline-flex items-center gap-1"><Search className="h-4 w-4"/> Søg</button>
          <Button size="sm" className="bg-yellow-300 text-black hover:bg-yellow-300/90 rounded-full h-7 px-3">Køb Plus</Button>
          <Button size="sm" variant="secondary" className="bg-white text-black hover:bg-white/90 rounded-full h-7 px-3">Log ind</Button>
        </div>
      </div>
    </div>
  );
}

/* ----------------------------------
   Inline tests (run in NODE_ENV=test)
   ---------------------------------- */
if (typeof process !== "undefined" && process.env && process.env.NODE_ENV === "test") {
  console.assert(sanitizeQuery("  hej  ") === "hej", "sanitize trims whitespace");
  console.assert(sanitizeQuery("hej\nverden") === "hej verden", "sanitize collapses newlines");
  console.assert(sanitizeQuery("") === "", "sanitize empty");
}
