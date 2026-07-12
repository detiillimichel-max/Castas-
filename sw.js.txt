const C='castas-v4-lite';const A=['./','./index.html','./chat.html','./manifest.json'];
self.addEventListener('install',e=>{e.waitUntil(caches.open(C).then(c=>c.addAll(A)));self.skipWaiting()});
self.addEventListener('activate',e=>e.waitUntil(caches.keys().then(k=>Promise.all(k.filter(x=>x!==C).map(x=>caches.delete(x))))));
self.addEventListener('fetch',e=>{
 if(e.request.url.includes('supabase')) return;
 e.respondWith(caches.match(e.request).then(r=>r||fetch(e.request).then(n=>{caches.open(C).then(c=>c.put(e.request,n.clone()));return n})).catch(()=>caches.match('./index.html')))
});
