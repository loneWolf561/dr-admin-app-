const CACHE_NAME = 'dr-admin-v1';
const urlsToCache = [
  '/dr-admin-app-/',
  '/dr-admin-app-/index.html',
  '/dr-admin-app-/manifest.json'
];

self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then((cache) => cache.addAll(urlsToCache))
  );
});

self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then((response) => {
        if (response) return response;
        return fetch(event.request);
      })
  );
});
  