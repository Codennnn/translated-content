---
title: CanvasRenderingContext2D.drawImage()
slug: Web/API/CanvasRenderingContext2D/drawImage
translation_of: Web/API/CanvasRenderingContext2D/drawImage
---
{{APIRef}}

La méthode **`CanvasRenderingContext2D.drawImage()`** de l'API 2D des Canvas instaure différentes manières de dessiner des images dans les balises canvas.

## Syntaxe

    void ctx.drawImage(image, dx, dy);
    void ctx.drawImage(image, dx, dy, dLargeur, dHauteur);
    void ctx.drawImage(image, sx, sy, sLargeur, sHauteur, dx, dy, dLargeur, dHauteur);

![drawImage](canvas_drawimage.jpg)

### Paramètres

- `image`
  - : Un élément à dessiner dans le contexte. La spécification autorise toute source d'image canvas ({{domxref("CanvasImageSource")}}), ainsi qu'une {{domxref("HTMLImageElement")}}, une {{domxref("HTMLVideoElement")}}, une {{domxref("HTMLCanvasElement")}} ou une {{domxref("ImageBitmap")}}.
- `dx`
  - : La coordonnée `x` dans le canvas de destination où placer le coin supérieur gauche de l'`image` source.
- `dy`
  - : La coordonnée `y` dans le canvas de destination où placer le coin supérieur gauche de l'`image` source.
- `dLargeur`
  - : La largeur de l'`image` dessinée dans le contexte de la balise canvas. Cela permet d'ajuster la taille de l'image. Si cet argument n'est pas spécifié, l'image prendra sa largeur normale.
- dHauteur
  - : La hauteur de l'`image` dessinée dans le contexte de la balise canvas. Cela permet d'ajuster la taille de l'image. Si cet argument n'est pas spécifié, l'image prendra sa hauteur normale.
- `sx`
  - : La coordonnée `x` du bord en haut à gauche de la partie de l'`image` source à dessiner dans le contexte du canvas.
- `sy`
  - : La coordonnée `y` du bord en haut à gauche de la partie de l'`image` source à dessiner dans le contexte du canvas.
- `sLargeur`
  - : La largeur de la partie de l'image source à dessiner dans le contexte. Si ce n'est pas spécifié, cet argument prend la valeur de la largeur de l'image moins `sx`, autrement dit l'image dessinée dans le contexte sera la partie de l'image d'origine à partir du point s de coordonnées (`sx`&nbsp;; `sy`) et jusqu'au bord en bas à droite.
- `sHauteur`
  - : La hauteur de la partie de l'image source à dessiner dans le contexte. De la même manière que pour sLargeur, si aucune valeur n'est donnée cet argument prendra la valeur de la hauteur de l'image moins `sy`.

### Exceptions

- `INDEX_SIZE_ERR`
  - : Si la balise canvas ou la largeur ou hauteur du rectangle source vaut zero ou moins.
- `INVALID_STATE_ERR`
  - : L'image reçue n'en est pas une.
- `TYPE_MISMATCH_ERR`
  - : L'image reçue n'est pas supportée.

## Exemples

### Utiliser la méthode `drawImage`

Ceci est un extrait de code utilisant la méthode `drawImage`&nbsp;:

#### HTML

```html
<canvas id="canvas"></canvas>
  <img id="source" src="rhino.jpg"
       width="300" height="227">
</div>
```

#### JavaScript

```js
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");
var image = document.getElementById("source");

ctx.drawImage(image, 33, 71, 104, 124, 21, 20, 87, 104);
```

Éditez le code suivant pour voir les changements en direct dans la balise canvas:

#### Code jouable

```html hidden
<canvas id="canvas" width="400" height="200" class="playable-canvas"></canvas>
  <img id="source" src="rhino.jpg" width="300" height="227">
</div>
<div class="playable-buttons">
  <input id="edit" type="button" value="Edit" />
  <input id="reset" type="button" value="Reset" />
</div>
<textarea id="code" class="playable-code">
ctx.drawImage(image, 33, 71, 104, 124, 21, 20, 87, 104);</textarea>
```

```js hidden
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");
var image = document.getElementById('source');
var textarea = document.getElementById("code");
var reset = document.getElementById("reset");
var edit = document.getElementById("edit");
var code = textarea.value;

function drawCanvas() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  eval(textarea.value);
}

reset.addEventListener("click", function() {
  textarea.value = code;
  drawCanvas();
});

edit.addEventListener("click", function() {
  textarea.focus();
})

textarea.addEventListener("input", drawCanvas);
window.addEventListener("load", drawCanvas);
```

{{ EmbedLiveSample('Code_jouable', 700, 360) }}

## Spécifications

| Spécification                                                                                                                                    | Statut                           | Commentaire |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------- | ----------- |
| {{SpecName('HTML WHATWG', "scripting.html#dom-context-2d-drawimage", "CanvasRenderingContext2D.drawImage")}} | {{Spec2('HTML WHATWG')}} |             |

## Compatibilité des navigateurs

{{Compat("api.CanvasRenderingContext2D.drawImage")}}

## Notes concernant la compatibilité

- Un support pour l'inversion de l'image pour les valeurs négatives pour `sLargeur` et `sHauteur` a été ajouté à Gecko 5.0 {{geckoRelease("5.0")}}.
- A partir de {{geckoRelease("5.0")}} `drawImage()` gère les arguments négatifs, conformément à la spécification, en inversant ces valeurs par rapport aux axes.
- Spécifier une image `null` ou `undefined` en appellant `drawImage()` correctement retournera une exception `TYPE_MISMATCH_ERR` à partir de {{geckoRelease("5.0")}}.
- Prior to Gecko 7.0 {{ geckoRelease("7.0") }}, Firefox ajoute une exception si une des coordonnées est nulle ou négative. Selon la spécification, cela ne durera pas.
- Gecko 9.0 {{ geckoRelease("9.0") }} supporte désormais correctement le CORS pour dessiner des images de domaines étrangers sans [corrompre le canvas](/fr/docs/Web/HTML/Images_avec_le_contr%C3%B4le_d_acc%C3%A8s_HTTP).
- Gecko 11.0 {{ geckoRelease("11.0") }} permet désormais de dessiner les images SVG dans le canvas sans [corrompre le canevas](/fr/docs/Web/HTML/Images_avec_le_contr%C3%B4le_d_acc%C3%A8s_HTTP).

## Notes

- drawImage() ne fonctionne correctement avec {{domxref("HTMLVideoElement")}} que si {{domxref("HTMLMediaElement.readyState")}} **est supérieur à 1.** (i.e, Chercher l'événement renvoyé après avoir mis la propriété currentTime)

## Voir aussi

- L'interface qui la définit, {{domxref("CanvasRenderingContext2D")}}.
