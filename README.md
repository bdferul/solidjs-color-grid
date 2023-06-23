## What is this?

A simple demonstration of how to update the state of a 2d array displayed with `<For>` tags. 

## With Signals

```jsx
const [grid, updateGrid] =
  createSignal([...Array(10)].map(_ =>
    [...Array(10)].map(_ =>
      Math.random() < .5)))

return <table><tbody>
  <For each={grid()}>{(row, y) => <tr>
    <For each={grid()[y()]}>{(cell, x) =>
      <td
        class={`${cell ? "bg-green-600" : 'bg-red-600'} w-8 h-8`}
        onClick={_ => {
          const val = [...grid()]
          val[y()][x()] = !val[y()][x()]
          updateGrid(val)
        }} />
    }</For>
  </tr>
  }</For>
</tbody></table>
```

## With Stores

```jsx
const [grid, updateGrid] =
  createStore([...Array(10)].map(_ =>
    [...Array(10)].map(_ =>
      Math.random() < .5)))

return <table><tbody>
  <For each={grid}>{(row, y) => <tr>
    <For each={row}>{(cell, x) =>
      <td
        class={`${cell ? "bg-green-600" : 'bg-red-600'} w-8 h-8`}
        onClick={_ => updateGrid(y(), x(), p => !p)} />
    }</For>
  </tr>
  }</For>
</tbody></table>
```