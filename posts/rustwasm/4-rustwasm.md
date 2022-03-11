# Rust/Wasm without npm

A couple weeks ago, I saw Rachel's Rust generative [art app](https://r4chel.github.io/art/) and since then, I've been gunning to make a Rust web app of my own. Like most Rust documentation, the go to [web app tutorial](https://rustwasm.github.io/docs/book/introduction.html) is informative and easy to follow. However, it assumes use of [npm](https://www.npmjs.com/) and a Javascript bundler whereas I wanted to avoid installing extra stuff. If for whatever reason that resonates with someone, maybe this post will be helpful.

## Some notes

The point of all this is to write performant stuff in Rust, compile it into webassembly (Wasm) using [```wasm-pack```](https://rustwasm.github.io/wasm-pack/installer/), and have your regular, bloated Javascript call on the Wasm to do heavy lifting. In order to expose Rust/Wasm functions so that they can be called from Javascript, we use the Rust crate [```wasm-bindgen```](https://crates.io/crates/wasm-bindgen) and annotate any Rust function we wish to export with ```#[wasm-bindgen]```.

Rather than following the tutorial's bloated Hello World, I recommend the [equivalent page](https://rustwasm.github.io/docs/wasm-bindgen/examples/hello-world.html) from the ```wasm-bindgen``` documentation, which also provides information on how to do without npm and Webpack. To compile to Wasm for immediate use, use the command ```wasm-pack build --target web```.

In addition to the resulting Wasm binary, ```wasm-pack``` will generate Javascript boilerplate, Typescript declaration files, and a ```package.json``` in a folder called ```pkg```. From what I can tell, most of this is for npm to build a package from. Without npm, it turned out the ```.wasm``` binary and the ```.js``` boilerplate was all I needed.


## Adjustments

Without npm, a few things change from the tutorial:

#### Javascript imports must specify the ```.js``` file and include the provided default ```init``` function
For instance,
```import init, { Universe, Cell } from './pkg/wasm_game_of_life.js';```
rather than
```import { Universe, Cell } from "wasm-game-of-life";```

#### The ```.wasm``` binary must be loaded in with the ```init()``` function before it is used
For example, if we exported a ```wordle``` function from Rust, we might write the following Javascript to use it:
```
import init, {wordle} from './pkg/wasm_wordle.js'

async function run() {
     await init();
     wordle();
}

run();
```

In case you're like me and don't know much Javascript and/or are very rusty, ```await``` can only be used in an ```async``` function and will halt the function until the statement finishes (more correctly: until a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) is settled, but this isn't super helpful for me to think about yet). In this case, that means ```wordle()``` will not be called until ```init()``` finishes loading in the webassembly that ```wordle()``` needs to run.

#### In order to access memory used by Wasm without npm, we need to save the output of the ```init()``` function
So instead of:
```
import { memory } from "wasm-wordle/wasm_wordle_bg";

...blah blah...
const wordleData = new Uint8Array(memory.buffer, dataPtr, dataLength);
```
something like:
```
import init, {wordle} from './pkg/wasm_wordle.js'

async function run() {
     let wasm = await init();
     
     ...blah blah...
     const wordleData = new Uint8Array(wasm.memory.buffer, dataPtr, dataLength);
}

run();
```

## Results
In the end, you've got a Wasm binary and a Javascript module to load it into whatever HTML document you've got. Like this one! I'm pretty excited to try this again with my own projects. I have some ideas involving audio processing and grammar parsing that might appreciate the speed boost of Rust and Wasm.

Anyhoo, below is the thing. I'll figure out how to CSS style it better later.