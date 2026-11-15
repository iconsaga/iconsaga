# Example: icons for a website section

**You ask** your AI (Claude Code, Codex or Cursor, with IconSaga connected):

> Add an icon to each of the three feature cards on the home page. Use our brand colors.

**Your AI:**

1. Looks for an icon for each card in plain words, like "launch fast", "secure payment" and "help chat".
2. Picks one style for the whole site, and saves each icon as its own small file in your project.
3. Gives the icons your text color, so they match the words next to them.

## What it adds to your page

For a site built with React and Tailwind, it looks something like this:

```tsx
import { RocketIcon } from "@/components/icons/RocketIcon";
import { ShieldCheckIcon } from "@/components/icons/ShieldCheckIcon";
import { ChatBubbleIcon } from "@/components/icons/ChatBubbleIcon";

const features = [
  { Icon: RocketIcon, title: "Live in a day", text: "Pick a template and publish." },
  { Icon: ShieldCheckIcon, title: "Safe payments", text: "Every order is protected." },
  { Icon: ChatBubbleIcon, title: "Real help", text: "Talk to a person, any time." },
];

export function Features() {
  return (
    <section className="grid gap-8 sm:grid-cols-3">
      {features.map(({ Icon, title, text }) => (
        <div key={title}>
          <Icon size={40} className="text-slate-900" />
          <h3 className="mt-4 font-semibold">{title}</h3>
          <p className="text-slate-600">{text}</p>
        </div>
      ))}
    </section>
  );
}
```

If you chose the two-color style, the second color is set once for every icon on the site:

```css
:root { --icon-accent: #FFB020; }
```

Not using React? Your AI asks for plain HTML instead and puts each icon straight into the page.

## The credit line

On the free plan, your AI adds this once, in the footer or on a credits page. With Pro, you don't need it.

<!-- sync:credit:block -->
```text
Icons by IconSaga · iconsaga.com
```
<!-- /sync -->
