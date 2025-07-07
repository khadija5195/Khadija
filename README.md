assignment-1/
├── app/
│   └── page.tsx
├── components/
│   ├── QuoteForm.tsx
│   └── QuoteList.tsx
├── data/
│   └── quotes.ts
├── lib/
│   └── utils.ts
├── public/
├── styles/
│   └── globals.css
├── tailwind.config.ts
├── shadcn.config.ts
├── tsconfig.json
├── package.json
└── README.md
export const quotes = [
  { topic: "motivation", text: "Push yourself, because no one else is going to do it for you." },
  { topic: "motivation", text: "The harder you work for something, the greater you’ll feel when you achieve it." },
  { topic: "motivation", text: "Dream bigger. Do bigger." },
  { topic: "life", text: "Life is what happens when you're busy making other plans." },
  { topic: "life", text: "Get busy living or get busy dying." },
  { topic: "life", text: "You only live once, but if you do it right, once is enough." },
];
'use client';

import { useState } from 'react';
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

export default function QuoteForm({ onSubmit }: { onSubmit: (topic: string) => void }) {
  const [topic, setTopic] = useState("");

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    onSubmit(topic);
  };

  return (
    <form onSubmit={handleSubmit} className="flex gap-4">
      <Input
        placeholder="Enter a topic (e.g., motivation)"
        value={topic}
        onChange={(e) => setTopic(e.target.value)}
        className="w-full"
      />
      <Button type="submit">Get Quotes</Button>
    </form>
  );
}
export default function QuoteList({ quotes }: { quotes: string[] }) {
  if (quotes.length === 0) {
    return <p className="mt-4 text-sm text-gray-500">No quotes found for that topic.</p>;
  }

  return (
    <ul className="mt-4 space-y-2">
      {quotes.map((quote, index) => (
        <li key={index} className="bg-muted p-4 rounded-md">
          “{quote}”
        </li>
      ))}
    </ul>
  );
}
'use client';

import { useState } from "react";
import QuoteForm from "@/components/QuoteForm";
import QuoteList from "@/components/QuoteList";
import { quotes as allQuotes } from "@/data/quotes";

export default function HomePage() {
  const [filteredQuotes, setFilteredQuotes] = useState<string[]>([]);

  const handleTopicSubmit = (topic: string) => {
    const matched = allQuotes
      .filter(q => q.topic.toLowerCase() === topic.toLowerCase())
      .map(q => q.text)
      .slice(0, 3);
    setFilteredQuotes(matched);
  };

  return (
    <main className="max-w-xl mx-auto py-12 px-4">
      <h1 className="text-2xl font-bold mb-6">Quote Generator</h1>
      <QuoteForm onSubmit={handleTopicSubmit} />
      <QuoteList quotes={filteredQuotes} />
    </main>
  );
}
# Assignment 1 - Quote Generator

A simple quote generator using Next.js, ShadCN UI, and local JSON data.

## How to run

```bash
# clone repo and go into folder
cd assignment-1

# install dependencies
npm install

# run dev server
npm run dev

---

### ✅ 6. Tailwind & ShadCN UI Setup

- You must run:

```bash
npx create-next-app@latest assignment-1 --typescript
cd assignment-1
npx shadcn-ui@latest init
npx shadcn-ui@latest add input
npx shadcn-ui@latest add button
