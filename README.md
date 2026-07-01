# Top 10 pour le Ballon d'Or

Widget interactif **drag & drop** : glisse 14 candidats pour composer ton Top 10 du
Ballon d'Or. Souris **et** tactile. Chaque joueur affiche son **club** et un **drapeau
de nationalité**.

## Données & photos

- **Photos joueurs** : API **Sportmonks** (CDN public, CORS activé → l'image partageable
  fonctionne sans héberger les fichiers). La clé API n'est pas exposée.

## Fonctionnalités

- Drag & drop unifié souris / tactile (colonne candidats scrollable)
- Partage **X / Facebook / WhatsApp**
- **Téléchargement d'une image PNG** du classement (canvas) + **partage natif** mobile
- Thème clair, accent or, responsive mobile (2 colonnes), auto-hauteur iframe
  (`postMessage` → `{type:'top10bdor-height'}`), `noindex,nofollow`

## Intégration WordPress (bloc « HTML personnalisé »)

```html
<h2>Compose ton Top 10 pour le Ballon d'Or</h2>
<p>De Kylian Mbappé à Lamine Yamal en passant par Ousmane Dembélé et Vitinha, classe
les 14 candidats et partage ton Top 10 du Ballon d'Or.</p>

<iframe
  id="top10-bdor"
  src="https://jcrochet-netizen.github.io/top10-ballon-dor/"
  title="Compose ton Top 10 pour le Ballon d'Or"
  loading="lazy"
  scrolling="no"
  referrerpolicy="strict-origin-when-cross-origin"
  style="width:100%;max-width:660px;display:block;margin:0 auto;border:0;overflow:hidden;min-height:1000px;"></iframe>

<script>
(function () {
  var ORIGIN = 'https://jcrochet-netizen.github.io';
  var frame  = document.getElementById('top10-bdor');
  window.addEventListener('message', function (e) {
    if (e.origin !== ORIGIN) return;
    var d = e.data;
    if (!d || d.type !== 'top10bdor-height') return;
    var h = parseInt(d.height, 10);
    if (!h || h < 1) return;
    if (!frame) frame = document.getElementById('top10-bdor');
    if (frame) frame.style.height = h + 'px';
  }, false);
})();
</script>
```

## Personnalisation

Tout est en haut du `<script>` de `index.html` : tableau `ITEMS` (joueur, club, pays,
drapeau, image Sportmonks), `CONFIG.shareUrl`, `CONFIG.hashtags`.
