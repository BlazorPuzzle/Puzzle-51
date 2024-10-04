# Blazor Puzzle #51

## Values That Bind

YouTube Video: https://youtu.be/oFtrPvwxd8I

Blazor Puzzle Home Page: https://blazorpuzzle.com

### The Challenge:

This is a simple Blazor Web App with Global Server Interactivity.

The Counter page shows an additional text input that's bound to a string.

When the counter is incremented, the string value is set to the counter's ToString() implementation.

Incrementing the counter updates the input box, until you enter a value then it stops working!

Can you fix it?

### The Solution:

This was a tricky one. This is the original non-working line 8 in *counter.razor*:

```html
<input @bind-Value=CounterString @bind-Value:event="oninput" />
```

The problem is that `Value` with an upper case is not the same as lower-case `value` , which is the solution:

```html
<input @bind-value=CounterString @bind-value:event="oninput" />
```

In general, lower-case property names apply to HTML elements, and Pascal-cased property names apply to Blazor components, or non-HTML elements.

Of course, if you omit `-value` from the `@bind` Blazor attribute will bind to the default property. So this:

```html
<input @bind=CounterString @bind:event="oninput" />
```

is the same as this:

```html
<input @bind-value=CounterString @bind-value:event="oninput" />
```

Boom!