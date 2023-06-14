# Sleeping Tabs

Some browsers have a tab freezing or sleeping feature to reduce computer resource usage for inactive tabs. This can cause SignalR connections to close and may result in an unwanted user experience. Browsers use heuristics to figure out if a tab should be put to sleep, such as:

- Playing audio
- Holding a web lock
- Holding an IndexedDB lock
- Being connected to a USB device
- Capturing video or audio
- Being mirrored
- Capturing a window or display
- Browser heuristics may change over time and can differ between browsers. Check the support matrix and figure out what method works best for your scenarios.

To avoid putting an app to sleep, the app should trigger one of the heuristics that the browser uses.

The following code example shows how to use a [Web Lock](https://developer.mozilla.org/docs/Web/API/Web_Locks_API) to keep a tab awake and avoid an unexpected connection closure.

```js
var lockResolver;
if (navigator && navigator.locks && navigator.locks.request) {
  const promise = new Promise((res) => {
    lockResolver = res;
  });

  navigator.locks.request("unique_lock_name", { mode: "shared" }, () => {
    return promise;
  });
}
```
