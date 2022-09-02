# node-resolve-flow
Isomorphic node resolve algorithm for any file system (in-browser or Node)

This module abstracts the node module resolution algorithm (loosely following the spec at https://nodejs.org/api/esm.html#esm_resolver_algorithm_specification, correcting its "imprecisions") as a flow (a generator function) given an abstract file system interface

Usage:
```js
import resolver from 'node-resolve-flow';

const resolve = resolver({ isFile, loadPkgJSON });
```

`resolve` will be a flow (a generator function) which takes 2 parameters: `importee` and `importer` and returning the file URL of the resolved module if successful, and throws or returns `undefined` if unsuccessful, where

- `isFile(fileURL)`: a user-supplied flow that should return true if object represented by `fileURL` exists and is a file
- `loadPkgJSON(fileURL)`: a user-supplied flow that should load the `package.json` file located at `fileURL`

**Note**: since the resolver is working with generators you would need a generator runner i.e [ConclureJS](https://github.com/dmaevsky/conclure) or [Redux Saga](https://redux-saga.js.org) to make use of it.
