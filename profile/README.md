<div align="center">

# GeaStack

**One TypeScript codebase, compiled native—from microcontrollers to consoles.**

TypeScript. JSX. Real CSS. Native binaries for every screen you ship on.

[Website](https://geastack.com) · [Docs](https://geastack.com/docs) · [Examples](https://github.com/geastack/examples) · [CLI](https://github.com/geastack/cli)

</div>

GeaStack is a native device UI stack for building product interfaces with
TypeScript, JSX, and real CSS, then compiling them ahead of time to native
binaries for microcontrollers, Linux and Windows desktops, macOS, iOS,
Android, and Xbox—and to native servers, where the same compiler turns
`node:http` applications into binaries.

The device runs no browser and no JavaScript VM. The compiled binary is the app.

## Watch It Run

[![CSS 3D cube running on ESP32 with GeaStack](https://img.youtube.com/vi/pC3kNSWaL18/maxresdefault.jpg)](https://www.youtube.com/watch?v=pC3kNSWaL18)

Real CSS transforms, perspective, and keyframes running natively on an ESP32-S3
AMOLED board.

## What A Gea App Looks Like

This is the shape of a Gea app: a small TypeScript store, a component class that
reads it, and normal CSS classes compiled into the native target.

`src/counter-store.ts`

```ts
import { Store } from '@geastack/core'

class CounterStore extends Store {
  count = 0

  decrement() { this.count = this.count - 1 }
  increment() { this.count = this.count + 1 }
  reset() { this.count = 0 }
}

export const counter = new CounterStore()
```

`src/App.tsx`

```tsx
import { ReactiveComponent } from '@geastack/core'
import { counter } from './counter-store'
import './styles.css'

export class App extends ReactiveComponent {
  template() {
    return (
      <div class="screen">
        <span class="eyebrow">GEASTACK</span>
        <span class="title">Shared store</span>
        <span class="count">{counter.count}</span>
        <div class="controls">
          <button class="button secondary" onClick={() => counter.decrement()}>−</button>
          <button class="button primary" onClick={() => counter.increment()}>+</button>
        </div>
        <button class="reset" onClick={() => counter.reset()}>Reset</button>
      </div>
    )
  }
}
```

`src/index.tsx`

```tsx
import { mount } from '@geastack/core'
import { App } from './App'

mount(App)
```

`src/styles.css`

```css
.screen {
  display: flex;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
  gap: 16px;
  align-items: center;
  justify-content: center;
  background-color: #080b12;
  color: #f8fafc;
}

.count {
  font-size: 76px;
  line-height: 1;
}

.controls {
  display: flex;
  flex-direction: row;
  gap: 16px;
}

.button {
  width: 92px;
  height: 58px;
  border-radius: 14px;
  border-width: 2px;
  font-size: 30px;
}
```

Create, set up, and flash an app with:

```sh
npx @geastack/create-geastack my-app
cd my-app
npx gea setup
npx gea flash --board <your-board> --monitor
```

`gea setup` walks you through your board, names it, and prints the exact
`gea flash` line to run—`<your-board>` is the alias you pick there.

Packages are published under the `@geastack` scope: `@geastack/create-geastack`
for project creation and `@geastack/cli` for the project-local CLI. Both keep
the product-facing commands as `create-geastack` and `gea`.

## Why GeaStack Exists

Modern hardware products usually become several UI products at once: one stack
for firmware, another for desktop tooling, another for mobile, and another for
web previews. GeaStack keeps the productive app model developers already
know—components, state, JSX, CSS, and Canvas-style drawing—and lowers it to
native targets.

| What you write | What GeaStack builds |
| --- | --- |
| TypeScript and JSX components | Target-native application code |
| Real CSS | Native layout, styling, animation, and media behavior |
| Canvas-style drawing | Native device draw calls for maps, charts, games, and dashboards |
| One app manifest | Web preview, ESP32-class boards, GeaOS/Linux, Windows, macOS, iOS, Android, and Xbox targets |

## Targets

| Target | Use it for |
| --- | --- |
| Web simulator | Fast local iteration and screenshots |
| ESP32 / ESP32-S3 / ESP32-P4 | Watches, panels, knobs, dashboards, and product UI bring-up |
| GeaOS | Linux-backed devices and shellable hardware targets |
| Linux desktop | Desktop apps and Raspberry Pi OS panels |
| macOS | Native desktop apps and companion tools |
| iOS | Native mobile apps and device companion experiences |
| Windows | Win32 desktop apps driven by real child-window controls |
| Android | Gea apps packaged as a native Android APK, rendered through a WebView |
| Node services | `node:http` servers compiled to native binaries |
| Xbox | Games and 3D scenes on a retail Series X/S in Dev Mode, through ANGLE on D3D11 |

## Start Here

For a new app:

```sh
npx @geastack/create-geastack my-app
cd my-app
npx gea setup
npx gea dev
```

For a Waveshare ESP32-S3 AMOLED board:

```sh
npx @geastack/create-geastack my-panel
cd my-panel
npx gea setup
npx gea flash --board <your-board> --monitor
```

For a richer example:

```sh
npx @geastack/create-geastack watch-demo --starter example --example watch
cd watch-demo
npx gea setup
npx gea flash --board <your-board> --monitor
```

## Repository Map

| Repository | Purpose |
| --- | --- |
| [`cli`](https://github.com/geastack/cli) | `gea` and `create-geastack`: project creation, setup, build, flash, monitor, examples, and diagnostics |
| [`core`](https://github.com/geastack/core) | App-facing API, runtime sources, UI engine scaffolding, host abstractions, and Gea compiler plugin |
| [`compiler`](https://github.com/geastack/compiler) | `geatsc`, the TypeScript-to-native compiler path |
| [`examples`](https://github.com/geastack/examples) | Example apps for web, ESP32, GeaOS, Windows, macOS, and iOS |
| [`tutorials`](https://github.com/geastack/tutorials) | Step-by-step learning paths for node and embedded targets |
| [`targets`](https://github.com/geastack/targets) | ESP32, RP2350, board metadata, device helpers, flash, monitor, OTA, and screenshots |
| [`apple`](https://github.com/geastack/apple) | macOS and iOS native targets |
| [`windows`](https://github.com/geastack/windows) | Native Windows (Win32) build target and Windows SDK bindings |
| [`android`](https://github.com/geastack/android) | Android WebView target |
| [`linux`](https://github.com/geastack/linux) | Native Linux desktop build targets |
| [`simulator`](https://github.com/geastack/simulator) | Web simulator and browser-based development loop |
| [`node-compat`](https://github.com/geastack/node-compat) | `node:http` applications compiled to native binaries |
| [`native-webgl-angle`](https://github.com/geastack/native-webgl-angle) | Native WebGL compatibility layer for the Three.js path |
| [`skills`](https://github.com/geastack/skills) | Agent skills for building GeaStack apps and targets |

## What Makes It Different

- **Ahead-of-time native output.** TypeScript, JSX, and CSS compile before the
  app reaches the device.
- **No browser dependency.** The target runs a native binary, not a webview.
- **One app model across product surfaces.** MCU displays, Linux panels,
  Windows and macOS desktops, mobile apps, console games, and native servers can
  share architecture and source patterns.
- **Real CSS where it matters.** Layout, transforms, animations, media queries,
  custom properties, gradients, shadows, and font rasterization are part of the
  native UI path.
- **Hardware-aware tooling.** Board selection, serial discovery, ESP-IDF setup,
  flashing, monitoring, OTA, screenshots, and target metadata are built into
  the CLI.

## Contributing

Contributing does not require memorizing the whole stack. Good first
contributions usually live at one boundary:

- improve an example app;
- add or verify board metadata;
- improve CLI diagnostics;
- document a hardware bring-up path;
- add tests around a target helper;
- polish docs where a first-time user would get stuck.

If you are bringing up a new board, start with:

```sh
npx gea setup
```

Choose `Custom board profile`, pick the closest base target, and save the
generated `.gea/boards/<alias>.json` profile with links to the schematic,
display controller, touch controller, storage, wireless, audio, GPS, and sensor
details.

## License

| Part | License |
| --- | --- |
| Framework, compiler, CLI, simulator, and the desktop, mobile, and Node targets | Apache-2.0 |
| Embedded board support—the [`targets`](https://github.com/geastack/targets) repository and `@geastack/chips` | GPL-3.0-only |
| Examples, tutorials, and skills | MIT |

The embedded board support is the only part under copyleft. Building a product
on the framework, the compiler, or the desktop, mobile, and Node targets carries
no obligation to publish your source.

- **Open-source firmware:** free.
- **Evaluation, prototypes, and internal devices:** free. The GPL's conditions
  apply when you distribute, not when you use.
- **Closed-source firmware shipped through the embedded target:** needs a
  commercial license. Contact [contact@geastack.com](mailto:contact@geastack.com).

## Links

- Website: [geastack.com](https://geastack.com)
- Docs and examples: [geastack.com/docs](https://geastack.com/docs)
- GitHub organization: [github.com/geastack](https://github.com/geastack)
