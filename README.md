## What is this?

A simple demonstration of how to update the state of a 2d array displayed with `<For>` tags. 

## With Signals

```jsx
const start = new Array(10).fill([]).map(_ => new Array(10).fill(false).map(_ => Math.random() * 10 < 5))
const [grid, updateGrid] = createSignal(start)

const flip = (x: number, y: number) => {
const val = [...grid()]
val[y][x] = !val[y][x]
updateGrid(val)
}

return <table>
<tbody>
    <For each={grid()}>{(row, y) => (
    <tr>
        <For each={grid()[y()]}>{(cell, x) => (
        <td
            class={`${cell ? "bg-green-500" : 'bg-red-500'} w-8 h-8`}
            onClick={_ => flip(x(), y())} />
        )}</For>
    </tr>
    )}</For>
</tbody>
</table>
```

## With Stores

```jsx
const [grid, updateGrid] = createStore(new Array(10).fill([]).map(_ => new Array(10).fill(false).map(_ => Math.random() * 10 < 5)))

return <table>
  <tbody>
    <For each={grid}>{(row, y) => (
      <tr>
        <For each={row}>{(cell, x) => (
          <td
            style={{ 'background-color': cell ? 'green' : 'red', width: '20px', height: '20px' }}
            onClick={_ => updateGrid(y(), x(), p => !p)}></td>
        )}</For>
      </tr>
    )}</For>
  </tbody>
</table>
```