const CACHE_NAME = "calculator-cache-v1";

const urlsToCache = [
  "./",
  "./index.html",
  "./manifest.json",
  "./192.png",
  "./512.png"
];

// Install event – cache all needed files
self.addEventListener("install", event => {
  event.waitUntil(
    caches.open(CACHE_NAME).then(cache => {
      return cache.addAll(urlsToCache);
    })
  );
});

// Fetch event – serve from cache when offline
self.addEventListener("fetch", event => {
  event.respondWith(
    caches.match(event.request).then(response => {
      return response || fetch(event.request);
    })
  );
});
